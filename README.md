Attacco a Metasploitable tramite la Vulnerabilità Java RMI

Passaggi Svolti

Configurazione dell'IP della macchina attaccante (Kali Linux) a 192.168.11.111
Configurazione dell'IP della macchina vittima (Metasploitable) a 192.168.11.112
Usando il comando:sudo ifconfig eth0 192.168.11.1xx netmask 255.255.255.0

Sfruttamento della Vulnerabilità:

Avviato Metasploit e cercato un exploit adatto per Java RMI

Utilizzato il modulo exploit/multi/misc/java_rmi_server per sfruttare la vulnerabilità

Configurati i parametri necessari (RHOSTS, LHOST, RPORT,HTTPDELAY) 

Lanciato l'exploit e ottenuto una sessione Meterpreter

Raccolta delle Informazioni:

Utilizzato i comandi ipconfig e route -n su Meterpreter per raccogliere informazioni sulla configurazione di rete e la tabella di routing della macchina vittima
il comando route mostra la tabella di routing di rete del sistema. La tabella di routing contiene informazioni su come il sistema deve instradare i pacchetti IP verso le varie reti
L'opzione -n fa in modo che il comando mostri l'output in formato numerico, evitando di risolvere gli indirizzi IP in nomi di host


SPIEGAZIONE Exploit e HTTPDELAY:

Cosa fa l'Exploit:
Il modulo si collega a un servizio RMI vulnerabile (sulla porta 1099) e invia un payload Java dannoso. Questo payload viene eseguito dalla macchina vittima, aprendo una connessione di ritorno (reverse shell) verso la macchina dell'attaccante, usando una sessione Meterpreter

L'exploit è pericoloso perché:

Non richiede autenticazione, quindi può essere eseguito facilmente se il servizio è esposto.
Consente l'esecuzione di codice remoto, dando il controllo completo della macchina bersaglio all'attaccante

Il parametro HTTPDELAY nell'exploit exploit/multi/misc/java_rmi_server di Metasploit specifica il tempo di attesa (in secondi) per il server HTTP integrato nel payload Java che viene inviato alla vittima
Quando si utilizza un payload Java, Metasploit avvia un server HTTP sulla macchina dell'attaccante
La macchina vittima, dopo essere stata sfruttata, si connette a questo server HTTP per scaricare il payload effettivo
HTTPDELAY determina quanto tempo il server HTTP rimane attivo, in attesa della connessione della vittima

Un valore di HTTPDELAY a 20 (come in questo caso) significa che il server HTTP rimane aperto per 20 secondi, consentendo alla vittima di connettersi e scaricare il payload
Impostare un ritardo adeguato (come 20 secondi) è utile per garantire che, in caso di latenze di rete o ritardi, il payload venga scaricato correttamente dalla macchina vittima senza problemi di timeout
Un valore troppo basso per HTTPDELAY(esempio 10), può causare un Denial of Service (DoS) se il tempo di attesa è basso durante l'attacco
