## T02: DRP – Implementació de les Còpies de Seguretat 💾🛠️

### Introducció 📝
En aquesta tasca posarem en pràctica la política de còpies per al client **Muntatges i Serveis Tècnics SL**, creant guies tècniques per Windows i Linux.  
L’objectiu és garantir còpies fiables, segures i recuperables seguint l’esquema **3-2-1**.

#

### [🟦 Part 1: Còpies de Seguretat en Windows 💻](./GUIES/GUIAWINDOWS.MD)

S’ha d’implementar una política especial per a l’equip del director, que necessita còpies locals i al núvol.

#

### Objectius 🎯
- Seguir l’esquema **3-2-1** (disc secundari + Google Drive).  
- Fer una **còpia cada hora local** ⏱️.  
- Fer **còpia al núvol a les 18:00h** ☁️.  
- Validar processos de restauració.

### Procediment 🛠️
1. Crear una **VM Windows 11** amb disc secundari de 10 GB.  
2. Instal·lar **Duplicati**.  
3. Configurar dos plans de còpia:
   - `Local` → **còpia horària.**  
   - `Google Drive` → **còpia diària a les 18:00.**  
4. Afegir fitxers, fer proves de còpia i restaurar tant localment com des del núvol.

---

### [🟩 Part 2: Còpies al Servidor Linux 🐧](./GUIES/GUIASERVER.MD)

Per al servidor s’utilitzarà **Duplicity** amb scripts i planificació via **cron**.

#

### Objectius 🎯
- Realitzar còpies completes i incrementals de `/home`.  
- Utilitzar un **disc auxiliar** muntat manualment.  
- Automatitzar les còpies amb **scripts** i **cron**.

### Procediment 🛠️
1. Afegir un disc, formatar-lo en **XFS** i muntar-lo a `/media/backup`.  
2. Instal·lar **duplicity**.  
3. Crear usuaris i fitxers de prova.  
4. Fer una còpia completa, restaurar-la i després fer una incremental.  
5. Crear els scripts:
   - `fullbackup.sh` → **diumenge 23:00**  
   - `incrementalbackup.sh` → **dilluns–dissabte 23:00**  
6. **Muntar abans de copiar** i **desmuntar al final** 🔒.

---
