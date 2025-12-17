## T09 – Servidor NFS
En aquest projecte configurarem un servidor NFSv3 i un client Linux per centralitzar fitxers dins d’un entorn empresarial. Crearem usuaris i grups, configurarem directoris compartits, aplicarem permisos, provarem opcions d’exportació com root_squash i establirem diferents nivells d’accés segons la xarxa. Finalment, configurarem el muntatge automàtic al client i valorarem les limitacions i millores possibles d’aquesta infraestructura.

### Fase 1 – Preparació de l'entorn

### **Maquinari virtual necessari**

* **Servidor:** Ubuntu Server 24.04 LTS  
* **Client:** Zorin OS 18

!(img)[../IMG/1.png]

### **Xarxes configurades**

* **NAT:** Accés a Internet  
* **Host-only:** Comunicació directa entre servidor i client, i possibilitat de connexió SSH al servidor  
  ![][image2]

### **Requisits i configuració inicial**

* Al servidor Ubuntu: habilitar **instal·lació del servei SSH** durant el setup  
  ![][image3]  
* Actualitzar els sistemes:

**`sudo apt update && sudo apt upgrade -y`**

**`![][image4]`**

Abans de començar qualsevol instal·lació, és essencial actualitzar el sistema per assegurar-nos que tenim les últimes versions dels paquets i correccions de seguretat. Aquest pas evita possibles conflictes amb dependències obsoletes.

### 

### **Configuració de xarxa**

sudo nano /etc/netplan/50-cloud-init.yaml

Configurar correctament les interfícies de xarxa és crucial per al funcionament del NFS. En aquest cas, s'han configurat dues interfícies: una per a Internet (dhcp4: true) i una per a la xarxa interna entre servidor i client.

### **Creació de grups**

sudo groupadd devs

sudo groupadd admins

![][image5]

### **Creació d'usuaris**

sudo useradd \-m \-s /bin/bash \-G devs dev01

sudo useradd \-m \-s /bin/bash \-G admins admin01

![][image6]

### **Assignació de contrasenyes**

Haurem d’entrar a \`\`cd /srv\`\` i assignar contrasenyes als usuaris prèviament creats

sudo passwd dev01

sudo passwd admin01

![][image7]

### **Creació de directoris compartits**

Es creen els directoris que es compartiran via NFS. La ruta /srv/nfs/ és la ubicació estàndard per a recursos compartits de xarxa. L'estructura separada permet organitzar diferents tipus de contingut.

sudo mkdir \-p /srv/nfs/dev\_projects

sudo mkdir \-p /srv/nfs/admin\_tools

![][image8]

### **Configuració de permisos**

sudo chown root:devs /srv/nfs/dev\_projects

sudo chmod 770 /srv/nfs/dev\_projects

sudo chown root:admins /srv/nfs/admin\_tools

sudo chmod 770 /srv/nfs/admin\_tools

 ![][image9]

Els permisos 770 (rwxrwx---) signifiquen que només el propietari (root) i el grup assignat tenen accés complet, mentre que altres usuaris no tenen cap accés. Això assegura que només els membres dels grups corresponents puguin accedir als seus directoris.

## **Fase 2: Instal·lació i Configuració del Servei NFS**

### **Instal·lació del servidor NFS**

S'instal·la el paquet nfs-kernel-server que proporciona la funcionalitat de servidor NFS. El sistema també instal·la automàticament les dependències necessàries com nfs-common, rpcbind, i keyutils.

sudo apt install nfs-kernel-server \-y

![][image10]

### **Configuració de les exportacions**

sudo nano /etc/exports

![][image11]

### **Inici i habilitació del servei**

sudo systemctl start nfs-kernel-server

sudo systemctl reload nfs-kernel-server

sudo systemctl enable nfs-kernel-server

![][image12]

### **Verificació de les exportacions**

La comanda exportfs \-u mostra totes les exportacions configurades. Es pot veure que ambdues carpetes estan disponibles per a tota la xarxa 192.168.56.0/24.

sudo exportfs \-u

### **Verificació de l'estat del servei**

sudo systemctl status nfs-kernel-server

### **Verificació dels grups creats**

La comanda getent group mostra la informació dels grups del sistema. Es pot veure que:

* devs té GID 1001 i conté l'usuari dev01  
* admins té GID 1002 i conté l'usuari admin01

Aquests GID seran importants per a la sincronització amb el client NFS.

getent group devs

getent group admins

![][image13]

## **Fase 3: Configuració del Client NFS**

## **Verificació de connectivitat**

## ping 192.168.56.112

 ![][image14]

\> La IP, la treiem del nostre enp0s8 del servidor.

### **Actualització del sistema client**

sudo apt update \-y && sudo apt upgrade \-y

Durant l'actualització, es configuren múltiples components del sistema incloent Ruby, biblioteques de xarxa, i paquets de seguretat. La regeneració del initramfs és necessària perquè el sistema pugui arrencar correctament després d'actualitzacions del kernel.

![][image15]

### **Instal·lació del client NFS**

sudo apt install nfs-common

![][image16]

El paquet nfs-common conté totes les eines necessàries per al client NFS, incloent:

* showmount: Per llistar recursos compartits  
* mount.nfs: Per muntar recursos NFS  
* nfsstat: Per estadístiques d'ús Les dependències instal·lades inclouen keyutils per a autenticació, libnfsidmap1 per a mapatge d'identificadors, i rpcbind per a comunicació RPC.

### **Verificació de recursos compartits**

sudo showmount \-e 192.168.56.112

![][image17]

La comanda showmount mostra que el servidor comparteix dos recursos:

* /srv/nfs/dev\_projects  
* /srv/nfs/admin\_tools El marcador "(everyone)" indica que aquests recursos estan disponibles per a tota la xarxa 192.168.56.0/24.

### **Creació de grups amb GID específics**

sudo groupadd \-g 1001 devs

sudo groupadd \-g 1002 admins

![][image18]

És crític que els GID coincideixin exactament entre servidor i client. El NFS identifica usuaris i grups pels seus identificadors numèrics (UID/GID), no pels noms. Si els números no coincideixen, els permisos no funcionaran correctament.

### **Creació d'usuaris amb UID específics**

sudo useradd \-m \-u 1001 \-g devs dev01

sudo useradd \-m \-u 1002 \-g admins admin01

![][image19]

Els UID també han de coincidir amb els del servidor:

* dev01: UID 1001, GID 1001 (grup devs)  
* admin01: UID 1002, GID 1002 (grup admins) Aquesta sincronització assegura que quan aquests usuaris accedeixin als recursos compartits, el servidor els reconegui correctament.

### **Assignació de contrasenyes**

sudo passwd dev01

sudo passwd admin01

![][image20]

### **Creació de punts de muntatge**

sudo mkdir \-p /mnt/admin\_tools

sudo mkdir \-p /mnt/dev\_projects

![][image21]

Els directoris /mnt/ són la ubicació estàndard per a dispositius i recursos muntats temporalment. La separació en dos directoris diferents permet organitzar l'accés als diferents tipus de recursos.

### **Muntatge del recurs admin\_tools**

sudo mount \-t nfs 192.168.56.112:/srv/nfs/admin\_tools /mnt/admin\_tools

![][image22]

La comanda mount estableix la connexió entre el recurs remot i el directori local. L'opció \-t nfs especifica el tipus de sistema de fitxers, i la sintaxi servidor:ruta indica quin recurs muntar.

### **Prova d'escriptura al recurs muntat**

sudo touch /mnt/admin\_tools/proval.txt

![][image23]

La creació d'un fitxer com a root demostra que el muntatge funciona i que tenim permisos d'escriptura. Aquest test valida que la connexió NFS està activa i que les opcions rw (read-write) a /etc/exports estan funcionant.

### **Verificació del fitxer creat**

ls \-l /mnt/admin\_tools

![Verificació fitxer][image24]

El fitxer proval.txt apareix amb propietari root:root i permisos 644\. Aquest és el comportament esperat quan s'utilitza root\_squash (opció per defecte), que converteix operacions de root del client en usuari nobody al servidor per seguretat.

### **Prova de remuntatge**

sudo umount /mnt/admin\_tools

sudo mount \-t nfs 192.168.56.112:/srv/nfs/admin\_tools /mnt/admin\_tools

sudo touch /mnt/admin\_tools/prova2.txt

![Desmuntatge][image25] ![Remuntatge][image26] ![Segona prova escriptura][image27]

Aquest procés de desmuntar i tornar a muntar demostra:

1. La fluïdesa en la gestió de recursos NFS  
2. Que els canvis es persisteixen al servidor  
3. La capacitat de restablir connexions sense reiniciar serveis

### **Interfície gràfica del client**

![][image28]

La interfície gràfica del Zorin OS mostra les ubicacions favorites i permet navegar pels recursos muntats. Aquesta és la forma en què els usuaris finals (desenvolupadors i administradors) interactuaran amb els recursos compartits.

## **Fase 4: Problemes d'Accés i Configuració Automàtica**

### **Problema d'accés des de l'explorador gràfic**

![][image29]

L'explorador gràfic mostra un error de permisos quan intenta accedir a /mnt/admin\_tools. Aquest problema succeeix perquè:

1. Els directoris muntats via NFS hereden els permisos del servidor  
2. L'explorador gràfic s'executa amb l'usuari client (UID 1000\)  
3. Els directoris al servidor tenen permisos 770 (rwxrwx---)  
4. L'usuari client no és membre dels grups devs o admins al servidor

Això demostra una limitació important del NFS sense autenticació centralitzada: els permisos depenen exclusivament dels UID/GID, i si no coincideixen exactament, l'accés es denega.

### **Configuració de muntatge automàtic**

sudo nano /etc/fstab

El fitxer /etc/fstab (File System Table) conté la informació dels sistemes de fitxers que s'han de muntar automàticament durant l'arrencada del sistema.

![][image30]

S'afegeixen dues línies al final del fitxer:

192.168.56.112:/srv/nfs/admin\_tools /mnt/admin\_tools nfs defaults 0 0

192.168.56.112:/srv/nfs/dev\_projects /mnt/dev\_projects nfs defaults 0 0

Explicació de cada camp:

1. Fitxer de sistema: 192.168.56.112:/srv/nfs/admin\_tools \- Recurs NFS remot  
2. Punt de muntatge: /mnt/admin\_tools \- Directori local on es muntarà  
3. Tipus: nfs \- Especifica que és un sistema de fitxers NFS  
4. Opcions: defaults \- Inclou rw, suid, dev, exec, auto, nouser, async  
5. Dump: 0 \- No fer còpies de seguretat amb dump  
6. Pass: 0 \- No verificar amb fsck en l'arrencada

### **Reinici del sistema client**

reboot

El reinici és necessari per provar la configuració de muntatge automàtic. Durant l'arrencada, el sistema llegeix /etc/fstab i intenta muntar tots els sistemes de fitxers especificats.

### **Verificació de muntatges després del reinici**

mount | grep nfs

Després del reinici, es comprova que els recursos NFS s'han muntat automàticament. La sortida mostra:

* Ambdós recursos estan muntats: /srv/nfs/admin\_tools i /srv/nfs/dev\_projects  
* Versió NFS: vers=4.2 \- S'utilitza la versió 4.2 del protocol  
* Opcions: rw,relative \- Lectura/escriptura amb temps relatius  
* Mides: rsize=524288,wsize=524288 \- Buffers de 512KB per optimitzar transferències  
* Seguretat: sec=sys \- Autenticació del sistema (basada en UID/GID)  
* Adreces: clientaddr=192.168.56.113, addr=192.168.56.112 \- Confirmació de la connexió entre client i servidor

### **Visualització dels directoris muntats a l'explorador**

![][image31]

L'explorador gràfic ara mostra les dues carpetes muntades (admin\_tools i dev\_projects) a la ubicació /mnt/. Tot i que l'explorador pot mostrar les carpetes, l'accés al contingut encara pot estar restringit per permisos.

### **Pantalla d'inici de sessió del client**

![][image32]

La pantalla d'inici de sessió mostra els tres usuaris configurats:

1. client: L'usuari principal del sistema client  
2. admin01: Usuari creat per a l'administració (grup admins)  
3. dev01: Usuari creat per al desenvolupament (grup devs)

Aquests usuaris poden iniciar sessió individualment per provar els permisos d'accés als recursos NFS des de diferents contexts d'usuari.

## **Anàlisi i Conclusions**

### **Èxits de la implementació:**

1. Servidor NFS configurat correctament: Exporta dos directoris amb permisos específics  
2. Client NFS funcionant: Pot muntar i accedir als recursos compartits  
3. Sincronització UID/GID: Els identificadors coincideixen entre servidor i client  
4. Muntatge automàtic configurat: Els recursos es munten automàticament en l'arrencada  
5. Connectivitat verificada: Ping i muntatges funcionen sense errors de xarxa

### **Limitacions identificades:**

1. Gestió manual d'usuaris: Cal crear usuaris manualment a totes les màquines  
2. Depenència de UID/GID: Els permisos fallen si els identificadors no coincideixen  
3. Seguretat bàsica: Sense autenticació centralitzada o xifrat  
4. Problemes amb explorador gràfic: L'accés des de GUI pot tenir problemes de permisos

### **Avaluació de la solució:**

La implementació demostra que el NFS és una solució viable per a centralitzar fitxers en entorns Linux, però requereix una gestió acurada dels permisos i identificadors d'usuari. Per a entorns petits com DevOptimize Solutions, aquesta solució pot ser suficient, però per a creixement futur es recomana migrar a una infraestructura més robusta amb autenticació centralitzada.

La prova de concepte està completada amb èxit: El client pot accedir als recursos compartits, els permisos funcionen segons els grups, i el muntatge automàtic assegura disponibilitat constant dels recursos.
