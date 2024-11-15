Passaggi Svolti

Configurazione dell'IP della macchina attaccante (Kali Linux) a 192.168.11.111
Configurazione dell'IP della macchina vittima (Metasploitable) a 192.168.11.112

Sfruttamento della Vulnerabilità:

Avviato Metasploit e cercato un exploit adatto per Java RMI

Utilizzato il modulo exploit/multi/misc/java_rmi_server per sfruttare la vulnerabilità

Configurati i parametri necessari (RHOSTS, LHOST, RPORT) 

Lanciato l'exploit e ottenuto una sessione Meterpreter

Raccolta delle Informazioni:

Utilizzato i comandi ipconfig e route -n su Meterpreter per raccogliere informazioni sulla configurazione di rete e la tabella di routing della macchina vittima

Cosa fa l'Exploit:
Il modulo si collega a un servizio RMI vulnerabile (sulla porta 1099) e invia un payload Java dannoso. Questo payload viene eseguito dalla macchina vittima, aprendo una connessione di ritorno (reverse shell) verso la macchina dell'attaccante, tipicamente usando una sessione Meterpreter

L'exploit è pericoloso perché:

Non richiede autenticazione, quindi può essere eseguito facilmente se il servizio è esposto.
Consente l'esecuzione di codice remoto, dando il controllo completo della macchina bersaglio all'attaccante
