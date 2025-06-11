# 📺 tvproxy

## 🚀 M3U8 Proxy Dockerizzato

Un server proxy leggero basato su **Flask** e **Requests**, progettato per:

- 📥 Scaricare e modificare flussi **.m3u / .m3u8**
- 🔁 Proxare i segmenti `.ts`, mantenendo header personalizzati
- 🚫 Superare restrizioni come **Referer**, **User-Agent**, ecc.
- 🐳 Essere facilmente **dockerizzabile** su qualsiasi macchina o server

---

## ☁️ Deploy su Render

1. Vai su **Projects → Deploy a Web Service → Public Git Repo**
2. Inserisci il repo: `https://github.com/nzo66/tvproxy` → **Connect**
3. Dai un nome a piacere
4. Imposta **Instance Type** su `Free`
5. Clicca su **Deploy Web Service**

---

## 🤗 Deploy su HuggingFace

`ricora di fare factory rebuild per aggiornare il proxy se ci sono aggiornamenti!`

1. Crea un nuovo **Space**
2. Scegli un nome qualsiasi e imposta **Docker** come tipo
3. Lascia **Public** e crea lo Space
4. Vai in alto a destra → `⋮` → **Files** → carica **DockerfileHF** rinominandolo **Dockerfile**
5. Infine vai su `⋮` → **Embed this Space** per ottenere il **Direct URL**

---

## 🐳 Docker (Locale o Server)

### ✅ Costruzione e Avvio

```bash
git clone https://github.com/nzo66/tvproxy.git
cd tvproxy
docker build -t tvproxy .
docker run -d -p 7860:7860 --name tvproxy tvproxy
```

---

## 🐧 Termux (Dispositivi Android)

### ✅ Costruzione e Avvio

```bash
pkg install git python -y
git clone https://github.com/nzo66/tvproxy.git
cd tvproxy
pip install -r requirements.txt'
gunicorn app:app -w 4 --worker-class gevent --worker-connections 100 -b 0.0.0.0:7860 --timeout 120 --keep-alive 5 --max-requests 1000 --max-requests-jitter 100
```

---

## 🐍 Avvio con Python (Locale)

### ✅ Setup e Avvio

```bash
# Clona il repository
git clone https://github.com/nzo66/tvproxy.git
cd tvproxy

# Installa le dipendenze
pip install -r requirements.txt

# Avvia il server
gunicorn app:app -w 4 --worker-class gevent --worker-connections 100 -b 0.0.0.0:7860 --timeout 120 --keep-alive 5 --max-requests 1000 --max-requests-jitter 100
```

---

## 🛠️ Gestione Docker

- 📄 Logs: `docker logs -f tvproxy`
- ⛔ Stop: `docker stop tvproxy`
- 🔄 Start: `docker start tvproxy`
- 🧹 Rimozione: `docker rm -f tvproxy`

---

## 🛠️ Come Utilizzare

Assicurati di sostituire i placeholder come `<server-ip>` con l'indirizzo IP o l'hostname effettivo del tuo server e `<URL_...>` con gli URL specifici.

---

### 1. Proxy per Liste M3U Complete 📡

Questo endpoint è progettato per proxare l'intera lista M3U. È particolarmente utile per garantire compatibilità e stabilità, con supporto menzionato per formati come Vavoo e Daddylive.

**Formato URL:**
```text
http://<server-ip>:7860/proxy?url=<URL_LISTA_M3U>
```

**Dove:**
-   `<server-ip>`: L'indirizzo IP o hostname del tuo server proxy.
-   `<URL_LISTA_M3U>`: L'URL completo della lista M3U che vuoi proxare.

> 📝 **Nota:** Questo endpoint è ideale per gestire l'intera collezione di flussi contenuta in un file M3U.

---

### 2. Proxy per Singoli Flussi M3U8 (con Headers Personalizzati) 📺✨

Questo endpoint è specifico per proxare singoli flussi video `.m3u8`. La sua caratteristica distintiva è la capacità di inoltrare headers HTTP personalizzati, essenziale per scenari che richiedono autenticazione specifica o per simulare richieste da client particolari.

**Formato URL Base:**
```text
http://<server-ip>:7860/proxy/m3u?url=<URL_FLUSSO_M3U8>
```

**Esempio:**
```text
http://<server-ip>:7860/proxy/m3u?url=https://example.com/stream.m3u8
```

**Dove:**
-   `<server-ip>`: L'indirizzo IP o hostname del tuo server proxy.
-   `<URL_FLUSSO_M3U8>`: L'URL completo del singolo flusso M3U8.

#### 🎯 Aggiungere Headers HTTP Personalizzati (Opzionale)

Per includere headers personalizzati nella richiesta al flusso M3U8, accodali all'URL del proxy. Ogni header deve essere prefissato da `&h_`, seguito dal nome dell'header, un segno di uguale (`=`), e il valore dell'header.

**Formato per gli Headers:**
```text
&h_<NOME_HEADER>=<VALORE_HEADER>
```

**Esempio con Headers Personalizzati:**
```text
http://<server-ip>:7860/proxy/m3u?url=https://example.com/stream.m3u8&h_user-agent=Mozilla/5.0...&h_referer=https://ilovetoplay.xyz/&h_origin=https://ilovetoplay.xyz
```

> ⚠️ **Attenzione:**
> - Ricorda di sostituire `Mozilla/5.0...` con lo User-Agent completo che intendi utilizzare.
> - Se i valori degli header contengono caratteri speciali (es. spazi, due punti), assicurati che siano correttamente URL-encoded per evitare errori.

---

## ✅ Caratteristiche

- 📁 Supporta **.m3u** e **.m3u8** automaticamente
- 🧾 Inoltra gli **HTTP Headers** necessari (Auth, Referer, etc.)
- 🔓 Supera restrizioni geografiche o di accesso
- 🖥️ Compatibile con **qualsiasi player IPTV**
- 🐳 Totalmente dockerizzato, pronto per il deploy
- 🐍 Avviabile anche direttamente con **Python**

---

## 🎉 Fine!

> Ora puoi guardare flussi M3U8 ovunque, senza restrizioni!  
> Enjoy the Stream 🚀