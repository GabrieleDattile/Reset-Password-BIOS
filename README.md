# Recupero della Password del BIOS e Sicurezza del Sistema

## Recupero della Password del BIOS

### Metodi Hardware:

- **Rimozione della Batteria:** Rimuovere la batteria della scheda madre per circa 30 minuti reimposta le impostazioni del BIOS, inclusa la password.
  ![remove-battery](https://github.com/GabrieleDattile/Reset-Password-BIOS/assets/137740496/98ca02e9-b249-45ae-9f5e-e19465d13712)

- **Jumper Reset:** Modificare un jumper sulla scheda madre per ripristinare le impostazioni del BIOS collegando pin specifici.
![cmos](https://github.com/GabrieleDattile/Reset-Password-BIOS/assets/137740496/75986522-c9cf-41c8-9975-d6e449ec95c1)

### Metodi Software:

- **Live CD/USB:** Utilizzare distribuzioni come Kali Linux per accedere a strumenti come [killCmos](https://www.majorgeeks.com/files/details/killcmos.html) e [CmosPWD](https://www.cgsecurity.org/wiki/CmosPwd) per il recupero della password del BIOS.

- **Utilizzo di Codici di Errore:** Inserire la password del BIOS in modo errato tre volte genera un codice di errore che può essere utilizzato per recuperare la password su siti web specializzati come [BIOS Password Recovery](https://bios-pw.org).

## Sicurezza UEFI

Per i sistemi moderni che utilizzano UEFI invece del BIOS tradizionale, lo strumento [chipsec](https://github.com/chipsec/chipsec) può essere utilizzato per analizzare e modificare le impostazioni UEFI, inclusa la disabilitazione del Secure Boot.

## Analisi della RAM e Attacchi Cold Boot

La RAM conserva i dati brevemente dopo l'interruzione dell'alimentazione, di solito per 1 o 2 minuti. Questa persistenza può essere estesa a 10 minuti applicando sostanze fredde, come azoto liquido. Durante questo periodo esteso, è possibile creare un dump di memoria utilizzando strumenti come [dd.exe](https://uranus.chrysocome.net/linux/rawwrite/dd-old.htm) e [Volatility](https://volatilityfoundation.org/about-volatility/).

## Attacchi di Accesso Diretto alla Memoria (DMA)

[INCEPTION](https://github.com/carmaa/inception) è uno strumento progettato per la manipolazione fisica della memoria tramite DMA, compatibile con interfacce come FireWire e Thunderbolt. Consente di bypassare le procedure di accesso effettuando una patch alla memoria per accettare qualsiasi password. Tuttavia, non è efficace contro i sistemi Windows 10.

## Accesso al Sistema tramite Live CD/USB

La modifica dei binari di sistema come sethc.exe o Utilman.exe con una copia di cmd.exe può fornire un prompt dei comandi con privilegi di sistema. Strumenti come [chntpw](https://www.kali.org/tools/chntpw/) possono essere utilizzati per modificare il file SAM di un'installazione di Windows, consentendo la modifica delle password.

[Kon-Boot](https://whatsoftware.com/login-to-windows-administrator-and-linux-root-account-without-knowing-or-changing-current-password/) è uno strumento che facilita l'accesso ai sistemi Windows senza conoscere la password modificando temporaneamente il kernel di Windows o UEFI.

## Gestione delle Funzionalità di Sicurezza di Windows

- **Scorciatoie di Avvio e Ripristino:**
  - `Supr`: Accedere alle impostazioni del BIOS.
  - `F8`: Accedere alla modalità di ripristino.
  - Premere `Shift` dopo il banner di Windows può bypassare l'autologon.

- **Dispositivi BAD USB:**
  - Dispositivi come Rubber Ducky e Teensyduino fungono da piattaforme per la creazione di dispositivi USB malevoli, in grado di eseguire payload predefiniti quando collegati a un computer di destinazione.

- **Copia Shadow del Volume:**
  - I privilegi di amministratore consentono la creazione di copie di file sensibili, inclusi il file SAM, tramite PowerShell.

- **Bypass dell'encryption BitLocker:**
  - L'encryption BitLocker può essere bypassata se la password di ripristino viene trovata all'interno di un file di dump di memoria (MEMORY.DMP). Strumenti come Elcomsoft Forensic Disk Decryptor o Passware Kit Forensic possono essere utilizzati per questo scopo.

- **Ingegneria Sociale per l'Aggiunta di una Chiave di Ripristino:**
  - Una nuova chiave di ripristino di BitLocker può essere aggiunta tramite tattiche di ingegneria sociale, convincendo un utente ad eseguire un comando che aggiunge una nuova chiave di ripristino composta da zeri, semplificando così il processo di decrittazione.

