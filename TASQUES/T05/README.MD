# 🔐 Projecte – Connexions SSH entre Clients Linux i Windows

## 📝 Descripció
En aquesta pràctica configurem un servidor SSH en Ubuntu i hi accedim des de Windows per aprendre a establir connexions remotes segures. Implementarem millores de seguretat com la desactivació del login de root, la restricció d’usuaris i l’ús de claus SSH. També configurarem un túnel SOCKS i comprovarem el trànsit amb Wireshark. 

---

## 🏗️ Fases del projecte

### 🖥️ Fase 1 – Preparació de l’Entorn
- Configuració de xarxa: NAT + Host-Only
- Instal·lació i activació del servei OpenSSH
- Comprovació d’estat del servei
<hr style="border:0.5px solid #ccc;" />


### 🪪 Fase 2 - Configuració i Seguretat del Servei SSH
- Edició del fitxer sshd_config
- Desactivació del login de root
- Limitació d’usuaris amb AllowUsers
- Reinici i validació de canvis
<hr style="border:0.5px solid #ccc;" />

### 🪟 Fase 3 – Connexió des de Windows
- Connexió SSH bàsica amb PowerShell
- Validació del host amb hostname
- Gestió d’errors d’autenticació i permisos
<hr style="border:0.5px solid #ccc;" />

### 🔀 Fase 4 – Creació d’un Túnel SOCKS
- Connexió SSH amb redirecció dinàmica
- Configuració del proxy a Windows
- Validació del trànsit a Wireshark
<hr style="border:0.5px solid #ccc;" />

### 🔑 Fase 5 – Accés sense Contrasenya (Claus SSH)
- Generació de claus SSH amb PowerShell
- Creació del directori .ssh al servidor
- Inserció i protecció de authorized_keys
- Connexió final utilitzant la clau privada

---

📎 Accés a la tasca
Tots els detalls, explicacions i captures estan disponibles a l’informe complet de la pràctica:

👉 [**Enllaç a la tasca**](./SOLUCIO.MD)
