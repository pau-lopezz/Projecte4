## T05: Accés Remot - Escriptori remot (RDP)

### Fase 1 – Preparació de l’Entorn
Primer, cal instal·lar i configurar les dues màquines, tant la de Windows com la de Zorin. Un punt important és la configuració de xarxa: a cada màquina haurem d’afegir dos adaptadors, un en mode NAT (per garantir connexió a Internet) i un en mode Xarxa d’Amfitrió (per permetre que ambdues màquines es puguin comunicar entre si).

![image](./IMG/1.png)

![image](./IMG/2.png)

---

### Fase 2 - Configuració i Seguretat del Servei SSH
A continuació, accedirem a la configuració de **Escritorio Remoto.** Allà activarem la primera opció. Un cop activada, es mostrarà el nom del nostre equip, informació que necessitarem més endavant per completar la configuració.

![image](./IMG/3.png)

<hr style="border:0.5px solid #ccc;" />

Quan ja tinguem l’opció activada i coneguem el nom del nostre ordinador, entrarem a la tercera opció que apareixia a la imatge: “Usuarios de escritorio remoto”. Aquest apartat serveix per indicar quins usuaris tindran permís per connectar-s’hi.

Aquí hi afegirem els usuaris de les dues màquines. En el cas de combinar un usuari de Windows amb un de Linux, ho escriurem d’aquesta manera:
```bash
USUARIWINDOWS\usuarilinux
```
![image](./IMG/4.png)

<hr style="border:0.5px solid #ccc;" />

Quan haguem afegit l’usuari a la màquina Windows, aquesta part quedarà configurada de moment. Ara passarem al Zorin. Obrirem l’aplicació “Remmina”, que ja ve instal·lada per defecte. Remmina és, en essència, el client d’escriptori remot que utilitza Linux. 

Un cop dins l’aplicació, al cercador de la part superior —com es veu a la imatge— escriurem el nom del PC de Windows, afegint-hi “.local” al final. En el meu cas, per exemple, l’adreça que he introduït és:
```bash
paulopezrdp.local
```
![image](./IMG/5.png)

<hr style="border:0.5px solid #ccc;" />

A continuació, apareixerà una finestra emergent amb les credencials RDP. Aquí haurem d’introduir l’usuari i la contrasenya corresponents al PC de Windows. Un cop feta l’autenticació, simplement premem “OK” per continuar.
![image](./IMG/6.png)

<hr style="border:0.5px solid #ccc;" />

Si hem completat tots els passos de manera correcta, la connexió remota s’establirà sense problemes i podrem accedir i utilitzar l’ordinador al qual ens estem connectant. A la imatge es pot veure que apareix “windowsrdp”, cosa que confirma que hem entrat al PC correcte i que la connexió s’ha configurat satisfactòriament.

---

### Fase 3 – Connexió des de Windows
Després d’haver establert la connexió de Zorin cap a Windows, passarem a la segona part, que consisteix a fer el procés invers: connectar-nos des de Windows al Zorin.

Per començar, obrirem la Configuració del Zorin i anirem a Sistema. Allà activarem les dos primeres opcions “Escriptori compartit” i “Control remot”. Cal tenir en compte que Zorin genera una contrasenya automàtica. És recomanable substituir-la per una contrasenya pròpia.
![image](./IMG/7.png)

<hr style="border:0.5px solid #ccc;" />
