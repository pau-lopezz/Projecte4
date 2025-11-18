## **Introducció**
La primera hora el vostre responsable de seguretat us presenta el tema de les còpies de seguretat a partir d’un material didàctic. A continuació, caldrà que hi treballeu els aspectes del tema i ho fareu mitjançant una dinàmica cooperativa.


## **Presentació del cas client**
"Muntatges i Serveis Tècnics SL" és una petita empresa dedicada a la instal·lació i manteniment d'equips industrials.

### **Infraestructura** **Tècnica**:

- Servidor de Fitxers (Ubuntu Server): Conté tota la documentació crítica:

    o   Documents de Projectes: Plànols, especificacions tècniques (300 GB, creixement moderat).

    o   Bases de Dades (Comptabilitat i Clients): Crítiques i d'ús diari (20 GB, canvi constant).

    o   Carpetes Personals dels Usuaris: Per a la feina diària (100 GB).

- 10 Equips Clients (Windows 10/11): Els usuaris treballen majoritàriament amb fitxers del servidor, però alguns tècnics guarden de forma temporal informes i altres arxius importants a la carpeta Documents.

-         Connexió a Internet: Fibra òptica de 600 Mbps (simètrica).

### **Requisits de Recuperació:**

-         Temps de Recuperació (RTO): Les dades de Comptabilitat/Clients han d'estar disponibles en menys de 4 hores.

-         Pèrdua de Dades Admesa (RPO): Es pot admetre una pèrdua màxima de 24 hores per a la majoria de dades, però les dades de Comptabilitat/Clients no poden perdre més de 4 hores de treball.

-         Retenció: Cal guardar les dades amb un historial d'almenys un mes.

---

### **Fase 1: Treball individual**

De forma individual, heu de donar resposta a les següents preguntes basant-se en el cas pràctic:

**1\.     Què copiar? (Priorització): Quines són les dades més crítiques del servidor? Cal fer còpia dels 10 equips clients? Justifica-ho.**

El més important de copiar són les bases de dades de Comptabilitat i Clients, perquè s’actualitzen constantment i l’empresa no es pot permetre perdre-les. També cal fer còpia dels documents de projectes i de les carpetes personals dels usuaris, ja que formen part del treball diari.

Sobre els 10 equips clients, no cal copiar-los sencers perquè gairebé tot ho treballen al servidor. Tot i això, és recomanable fer còpia de la carpeta **Documents** de cada equip, perquè alguns tècnics hi guarden arxius temporals que poden ser útils.

#

**2\.  Periodicitat i Tipus de Còpia: Proposa un calendari bàsic per a la setmana (Diari/Setmanal/Mensual) i quin tipus de còpia aplicaràs (Completa, Diferencial, Incremental) per a les dades crítiques.**

La proposta és fer una còpia completa cada divendres i còpies incrementals de dilluns a dijous per anar guardant només els canvis del dia.

A més, les bases de dades necessiten una protecció especial: es farà una còpia cada 4 hores per evitar perdre més informació de la que permet el RPO.

#

**3\.     Mitjans i Ubicació: Quin tipus de mitjà de còpia utilitzaries (Discs durs externs, NAS, Cloud, Cintes)? On s'hauria de guardar físicament la còpia més recent (Regla 3-2-1).**

Per aplicar correctament la regla 3-2-1, la millor opció és combinar diferents tipus de mitjans i ubicacions: per exemple, un NAS dins de l’empresa i una còpia al núvol.

- **Mitjans de còpia:**

   1. **NAS**: Permet tenir les còpies més recents i recuperar-les ràpidament en cas de fallada local.

   2. **Cloud**: Actua com a còpia offsite, protegint les dades davant incendis, robatoris o avaries greus.

- **Ubicació segons la regla 3-2-1:**

   3. **Dades originals**: al servidor de l’empresa.

   4. **Còpia 1**: al NAS dins de l’empresa (mitjà diferent del servidor).

   5. **Còpia 2**: al núvol (ubicació fora de l’empresa, mitjà diferent).

La còpia més recent hauria d’estar al **NAS**, ja que permet una restauració ràpida en cas de necessitat, mentre que la còpia al núvol assegura la recuperació davant desastres que afectin l’empresa.
