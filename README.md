Passaggi Svolti

Configurazione dell'IP della macchina attaccante (Kali Linux) a 192.168.11.111.
Configurazione dell'IP della macchina vittima (Metasploitable) a 192.168.11.112.

Sfruttamento della Vulnerabilità:

Avviato Metasploit e cercato un exploit adatto per Java RMI.

Utilizzato il modulo exploit/multi/misc/java_rmi_server per sfruttare la vulnerabilità.

Configurati i parametri necessari (RHOSTS, LHOST, RPORT) 

Lanciato l'exploit e ottenuto una sessione Meterpreter.

Raccolta delle Informazioni:

Utilizzato i comandi ipconfig e route -n su Meterpreter per raccogliere informazioni sulla configurazione di rete e la tabella di routing della macchina vittima.

Descrizione della Vulnerabilità:

La vulnerabilità sfruttata è legata a Java RMI, un protocollo che consente di invocare metodi su oggetti Java remoti, rendendo possibile l'interazione tra programmi distribuiti su diverse macchine. 
Il problema risiede nella mancanza di controlli di sicurezza adeguati nel servizio Java RMI su Metasploitable, che permette a un attaccante di caricare ed eseguire codice arbitrario sulla macchina vittima tramite un exploit apposito.
Questa vulnerabilità consente di ottenere l'accesso remoto alla macchina bersaglio, aprendo una sessione di Meterpreter, da cui è possibile eseguire ulteriori comandi e raccogliere informazioni sensibili.
