## T02: DPR: còpies de seguretat

## Part 2: Còpia seguretat servidor Linux

### Introducció
Per fer les còpies del servidor Linux la solució proposada pel vostre responsable és Duplicity que permet fer còpies tant contra un mitjà local o un servidor remot. Combinat amb el programador de tasques (cron) es poden implementar les polítiques de còpia que es desitgin.

---
Per començar, necessitarem una màquina virtual amb Zorin instal·lat. A aquesta màquina li afegirem un segon disc de 10 GB que simula una unitat auxiliar, la qual utilitzarem per fer còpies de seguretat i provar la gestió de dades.

![image](../IMG/l1.png)

<hr style="border:0.5px solid #ccc;" />

Quan accedim a la màquina, podem comprovar amb ``lsblk`` que el disc addicional està sent detectat.

![image](../IMG/l2.png)

> Nota important: Si no tenim fdisk haurem d’instal·lar-lo amb ``sudo apt install fsdisk``

<hr style="border:0.5px solid #ccc;" />

Crearem una nova partició al disc addicional ``sdb`` utilitzant la comanda següent. Aquesta acció ens permetrà definir un espai d’emmagatzematge independent dins del disc que després podrem formatar i muntar per utilitzar-lo com a unitat auxiliar.

```bash
sudo fdisk /dev/sdb
```` 

![image](../IMG/l3.png)

<hr style="border:0.5px solid #ccc;" />

Un cop aparegui el menú, seguirem les següents instruccions:

- ``n`` → Crear una nova partició

- p → Definir-la com a partició primària

- Enter → Acceptar el número de partició per defecte

- Enter → Acceptar el primer sector per defecte

- Enter → Acceptar l’últim sector per defecte

- w → Guardar els canvis i sortir del menú
