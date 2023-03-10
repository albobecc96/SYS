Useful reminders of SYS library

Il modulo sys
Questo modulo è uno dei pacchetti base, incluso nella Python Standard Library. Quindi una volta installato Python (sia la versione 2.7.x che la 3.x.x) sarà sufficiente scrivere

import sys

per poterlo importare nel nostro codice.

Questo modulo contiene una serie di funzioni e parametri che risulteranno molto utili ogni volta che il nostro programma dovrà interagire con il sistema operativo su cui si sta lavorando. Questo ci permetterà di lavorare su file system, ottenere informazioni varie sul sistema operativo ed effettuare altre operazioni, senza doverci preoccupare molto del sistema operativo su cui stiamo lavorando.

Per esempio è molto semplice ottenere informazioni sulla versione dell’interprete Python su cui stiamo lavorando.

sys.version

Se invece vogliamo utilizzare questi valori per futuri controlli nel nostro programma conviene utilizzare

sys.version_info
che restituisce i valori separati in diversi attributi, in modo da poterli utilizzare come singole variabili di controllo nel corso del programma.


Argomenti per gli script eseguiti a riga di comando
Uno degli utilizzi principali di questo modulo, è per gli script. Infatti spesso da riga di comando, quando dobbiamo lanciare l’esecuzione di un programma in Python, si preferisce passare degli argomenti, od opzioni in questo caso, allo script, invece di modificare ogni volta i valori delle variabili all’interno del codice. Inoltre il creare gli script in questo modo li rende consoni agli altri comandi di shell lanciati attraverso riga di comando.

Gli argomenti passati per riga di comando saranno racchiusi all’interno di sys.argv sotto forma di una lista. Il primo elemento di questa lista è il nome dello script stesso. Gli altri elementi seguono l’ordini di immissione per riga di comando.


Scrivete il codice seguente e salvatelo come myscript.py.

#!/usr/bin/python
import sys

print "Script name: %s" % sys.argv[0]
for i in range(len(sys.argv)):
if i > 0:
print "Arg%d: %s"% (i, sys.argv[i])
Eseguendo questo script e passandogli una serie di argomenti si ottiene:


Modificare il comportamento di output della shell di Python
Uno degli aspetti peculiari della programmazione in Python è la possibilità di lavorare in modalità interattiva. Attivando una shell di Python è possibile introdurre una riga di codice alla volta e attendere il risultato per poi inserire la successiva. Ogni volta che inseriamo un comando, la shell mostra un output significativo del risultato dell’operazione richiesta.

Aprendo una sessione in Python ed inserendo un comando, per esempio l’assegnazione di un valore ad una variabile otteniamo:

module sys displayhook
Questo è il comportamento di default di una sessione di Python, comunque a volte potresti aver bisogno di un comportamento differente. Per modificare questo comportamento si utilizza sys.displayhook. Si passa una funzione da noi definita che modifica questo comportamento di default.

import sys

def new_display(x):
 print "out: ", x

sys.displayhook = my_display
module sys - displayhook
Standard Data Streams
Tutti quelli che hanno un minimo di familiarità con sistemi operativi come Linux o Unix sanno già di che cosa stiamo parlando. Infatti gli standard data stream (noti anche come pipes) sono tre, uno per i valori in input (stdin), uno per i messaggi in output (stdout) ed uno per i messaggi di errore (stderr).

Con Python, grazie proprio al modulo sys, è possibile accedere direttamente a questi data stream mediante sys.stdin, sys.stdout e sys.stderr.

sys.stdout.write("This is the output stream\n")
questo comando invia una stringa sul data stream in output


Per quanto riguarda l’input, per esempio, possiamo passare nel data stream di input una stringa che ci verrà richiesta successivamente al comando seguente

x = sys.stdin.readline()[:-1]
Inseriamo una stringa che verrà immagazzinata nella variabile x, con [:-1] eliminiamo dalla stringa il carattere di newline alla fine.

module sys - data stream stdin stdout stderr
Se invece vogliamo inserire un messaggio di errore da inserire nel data stream di errore:

sys.stderr.write(“This is the error message\n”)


Le I/O Redirections
Abbiamo appena visto gli Standard Data Stream e come è possibile utilizzarli tramite il modulo sys. Un altro caso correlato ad essi sono le I/O redirections. Questa tecnica è molto utilizzata per chi lavora sulle shell di Linux o di Unix.
Infatti gli standard data stream possono essere reindirizzati su di un file per effetturare una lettura od una scrittura su di esso. Anche lo stderr spesso viene reindirizzato su di un file per creare un log file su cui successivamente si potranno controllare eventuali messaggi di errore.

Per esempio, creiamo un file redirect.py ed inserisci il codice seguente:

import sys

sys.stdout.write("This is the output message\n")
sys.stderr.write("This is the error message\n")
Se adesso eseguirete il programma con le redirections su due file di log

python redirect.py > output.log 2> error.log
Troverete all’interno dei due file i messaggi corrispondenti.

Bene tutto questo è possibile effettuarlo direttamente con Python all’interno del programma stesso.


Create un file redirect.py ed inserite il codice seguente.

import sys

save_stdout = sys.stdout
save_stderr = sys.stderr
file1 = open("output.log","w")
file2 = open("error.log","w")
sys.stdout = file1
sys.stderr = file2
print("This is the output message\n")
sys.stderr.write("This is the error message\n")
sys.stdout = save_stdout
sys.stderr = save_stderr
file1.close()
file2.close()
Alcuni parametri interessanti
All’interno del modulo sys esistono alcuni attributi che ci permettono di conoscere alcuni parametri interessanti che potrebbero a volte essere utili.

Per esempio

sys.executable

questo attributo restituisce il path dell’interprete di Python su cui stiamo eseguendo il programma

module sys - executable
sys.maxint

Questo attributo restituisce il più grande numero intero positivo supportato da Python. (Per ottenere il più grande valore negativo intero si utilizza lo stratagemma “- maxint – 1”)


sys.modules

Questo dizionario contiene tutti i moduli che sono stati caricati dall’interprete di Python.

Se vogliamo accedere ad un modulo in particolare possiamo scrivere


sys.path

Questo attributo è una lista contenente tutti le directory dove Python cerca per i moduli.


sys.platform 

Questo attributo restituisce il nome della piattaforma (sistema operativo) su cui Python sta lavorando

module sys - platform
sys.getrecursionlimit()

sys.setrecursionlimit(limit)

Queste due funzioni sono utili per vedere ed impostare il limite di ricorsioni possibili accettate dall’interprete Python. Questo valore è utile per impedire ricorsioni infinite che provocherebbero l’arresto del sistema.

module sys - recursion limit
Conclusioni
In questo articolo abbiamo visto una panoramica delle caratteristiche essenziali e degli strumenti forniti da questo importante modulo appartenente alla Python Standard Library. Spero che sia stato utile e che queste informazioni possano migliorare il vostro approccio con il mondo della programmazione in Python.
