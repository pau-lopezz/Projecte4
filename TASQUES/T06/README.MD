# 🔐 Projecte – Connexions SSH entre Clients Linux i Windows

## 📝 Descripció
En aquesta pràctica configurarem un entorn de suport remot utilitzant Remote Desktop Protocol (RDP) per permetre connexions bidireccionals entre Windows i Zorin OS.
Primer prepararem les màquines virtuals i la xarxa, i després establirem dues connexions remotes:

**Zorin OS → Windows**

**Windows → Zorin OS**

Aquesta pràctica simula situacions reals de suport tècnic on el consultor ha de prendre control del dispositiu d’un client.

---

## 🏗️ Fases del projecte

### 🖥️ Fase 1 – Preparació de l’Entorn
- Configurar màquines Windows i Zorin
- Configuració de xarxa: NAT + Host-Only
<hr style="border:0.5px solid #ccc;" />


### 🪪 Fase 2 - Configuració i Seguretat del Servei SSH
- Activar Escritorio Remoto a Windows
- Afegir usuaris autoritzats
- A Zorin, obrir Remmina i connectar a nomPC.local
- Introduir credencials i validar connexió
<hr style="border:0.5px solid #ccc;" />

### 🪟 Fase 3 – Connexió des de Windows
- A Zorin, activar Escriptori Compartit i Control Remot
- Canviar la contrasenya generada i reiniciar
- A Windows, obrir Conexión a Escritorio Remoto i connectar a hostname.local
- Acceptar certificat i iniciar sessió

---

📎 Accés a la tasca
Tots els detalls, explicacions i captures estan disponibles a l’informe complet de la pràctica:

👉 [**Enllaç a la tasca**](./SOLUCIO.MD)
<hr style="border:0.5px solid #ccc;" />

🖼️ Imatges de la pràctica

Totes les captures utilitzades en aquesta pràctica estan disponibles a la carpeta d’imatges del projecte:

📁 [**Enllaç a la carpeta**](./IMG)
