## T05: Accés Remot - Escriptori remot (RDP)

### Fase 1 – Preparació de l’Entorn
Primer, cal instal·lar i configurar les dues màquines, tant la de Windows com la de Zorin. Un punt important és la configuració de xarxa: a cada màquina haurem d’afegir dos adaptadors, un en mode NAT (per garantir connexió a Internet) i un en mode Xarxa d’Amfitrió (per permetre que ambdues màquines es puguin comunicar entre si).

![image](./IMG/1.png)

![image](./IMG/2.png)

---

### Fase 2 - Configuració i Seguretat del Servei SSH
A continuació, accedirem a la configuració de **Escritorio Remoto.** Allà activarem la primera opció. Un cop activada, es mostrarà el nom del nostre equip, informació que necessitarem més endavant per completar la configuració.

![image](./IMG/3.png)

Quan ja tinguem l’opció habilitada i sapiguem el nom del nostre ordinador, haurem d’anar a la tercera secció que apareixia a la imatge anterior: “Usuarios de escritorio remoto”. En aquest espai és on indicarem quins usuaris poden accedir-hi. Simplement hem d’afegir-hi els usuaris que utilitzarem tant a la màquina Windows com a la de Zorin, perquè tots dos tinguin permís per connectar-se.
