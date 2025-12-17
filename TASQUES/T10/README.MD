## 🖨️ T10 — Servidor d’impressió Linux (CUPS)

En aquesta pràctica es realitza la configuració d’un **servidor d’impressió en xarxa utilitzant CUPS (Common UNIX Printing System)**, el sistema estàndard d’impressió en entorns Linux. La implementació es basa en una arquitectura **client–servidor**, on un equip centralitza la gestió de les impressores i la resta d’equips hi accedeixen a través de la xarxa.

L’objectiu principal de la tasca és **compartir una impressora virtual** des del servidor i comprovar que els clients poden afegir-la i enviar treballs d’impressió correctament. D’aquesta manera, es simula un entorn real d’empresa on diversos usuaris imprimeixen mitjançant un únic servidor.

Durant la pràctica es treballa amb **dues màquines virtuals**: un servidor amb *Ubuntu Server*, encarregat de gestionar el servei CUPS, i un client amb *Zorin OS*, que es connecta al servidor per utilitzar la impressora compartida.

---

### 📌 Fases de la pràctica
1. Instal·lació del servei **CUPS** al servidor.  
2. Instal·lació d’una **impressora virtual PDF**.  
3. Configuració de CUPS i accés des de la xarxa.  
4. Compartició de la impressora mitjançant el frontal web.  
5. Afegir la impressora des del **client Zorin OS**.  
6. Realitzar proves d’impressió des del client.  
7. Verificar al servidor la generació dels **fitxers PDF**.

Aquesta tasca permet entendre de manera pràctica el funcionament d’un **servidor d’impressió Linux**, la gestió de permisos d’usuari i el flux complet d’impressió en un entorn de xarxa.

---

