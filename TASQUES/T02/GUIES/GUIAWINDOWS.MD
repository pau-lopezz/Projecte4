## T02: DPR: còpies de seguretat

## Part 1: Còpia seguretat dels equips clients Windows

### 1. Introducció
Aquesta guia descriu com protegir la informació de l’ordinador Windows del director mitjançant una política de còpies de seguretat basada en el model 3-2-1. El sistema combina una còpia local al disc secundari de l’equip i una còpia externa al núvol a través de Google Drive utilitzant Duplicati.

L’objectiu és garantir que les dades més importants de l’usuari —especialment els fitxers de Documents— estiguin sempre disponibles i es puguin recuperar fàcilment en cas d’error, pèrdua o eliminació accidental.

---

### 2. Requisits previs
Per dur a terme la configuració, es treballarà amb una màquina virtual amb Windows 11 que disposa de dos discs durs:
- Disc principal, on s’instal·la el sistema operatiu.
- Disc secundari de 10 GB, formatat en NTFS i utilitzat com a unitat addicional (per exemple, D:).


A més, cal disposar d’un compte personal de Google amb accés a Google Drive, un usuari local de Windows per gestionar l’equip i connexió a Internet, necessària tant per instal·lar Duplicati com per sincronitzar les còpies de seguretat amb el núvol.


<hr style="border:0.5px solid #ccc;" />
