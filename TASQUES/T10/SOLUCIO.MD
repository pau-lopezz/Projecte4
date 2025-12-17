## T10: Servidor impressió Linux. CUPS 

### Escenari de Treball
Màquina 1 (Servidor): Ubuntu Server configurat amb dues interfícies de xarxa: una en mode NAT i una segona en Host-Only.

![image](./IMG/1.png)

Màquina 2 (Client): Zorin OS (Desktop) configurat amb la mateixa estructura de xarxa que el servidor, utilitzant NAT i Host-Only.

![image](./IMG/2.png)

---

### 1. Instal·lació de CUPS al servidor

Abans d’instal·lar CUPS, és necessari actualitzar el sistema operatiu per assegurar-nos que disposem de les últimes versions dels paquets i correccions de seguretat. Això ajuda a evitar possibles incompatibilitats i garanteix una instal·lació més estable del servei.

```bash
sudo apt update -y && sudo apt upgrade -y
```

![image](./IMG/3.png)

---

Un cop finalitzada l’actualització del sistema, procedim a instal·lar CUPS, ja que és el servei necessari per gestionar les impressores al servidor.

```bash
sudo apt install cups -y
```

![image](./IMG/4.png)

---

### 2. Instal·lar impressora virtual

Per instal·lar la nostra impressora virtual, accedim com a usuari root al client amb ``sudo su`` i instal·lem el paquet cups-pdf, que permet crear una impressora virtual que genera arxius PDF en lloc d’impressions físiques.

```bash
apt install cups-pdf
```

![image](./IMG/5.png)
![image](./IMG/6.png)
![image](./IMG/7.png)
![image](./IMG/8.png)
![image](./IMG/9.png)
![image](./IMG/10.png)
![image](./IMG/11.png)
![image](./IMG/12.png)
![image](./IMG/13.png)
![image](./IMG/14.png)
![image](./IMG/15.png)
![image](./IMG/16.png)
![image](./IMG/17.png)
![image](./IMG/18.png)
![image](./IMG/19.png)
![image](./IMG/20.png)
![image](./IMG/21.png)
![image](./IMG/22.png)
![image](./IMG/23.png)

