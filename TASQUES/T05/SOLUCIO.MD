## T05: Accés Remot - Connexió via SSH

Per a aquesta pràctica necessitarem dues interfícies de xarxa: NAT i Adaptador només
amfitrió
![image](./IMG/image1.png)

---

Per instal·lar SSH, primer actualitzem el sistema amb: 
```bash 
sudo apt upgrade && sudo apt update
```
![image](./IMG/image2.png)

---

Un cop hagin acabat l’update i l’upgrade, ja podem instal·lar SSH.
```bash 
sudo apt install ssh -y
```

---

És molt important iniciar el servei SSH i comprovar-ne l’estat. Per això fem:
```bash 
sudo systemctl start ssh
sudo systemctl status ssh
```
