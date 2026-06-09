# Progetti di Studio: Machine Learning & Cybersecurity

Questo repository funge da mio blocco note e hub personale per tracciare i progressi nello studio del Machine Learning applicato alla Cybersecurity e nella gestione del mio percorso formativo. I progetti inclusi spaziano dallo sviluppo di interfacce web per il tracciamento dello studio all'implementazione di modelli di intelligenza artificiale per il rilevamento di intrusioni informatiche.

-------------------------------------------

## 1. NLP SPAM CLASSIFIER con NAIVE BAYES

I messaggi di spam e i tentativi di phishing sono ormai all'ordine del giorno. Ho voluto capire come funzionano i filtri automatici creando una pipeline che:
1. Prende un testo grezzo e lo pulisce.
2. Lo trasforma in numeri (visto che i computer non leggono le parole come noi).
3. Usa un algoritmo probabilistico per decidere se il messaggio è sicuro o sospetto.

Questo repository serve come mio blocco note per tracciare i progressi nell'uso di librerie come `pandas`, `scikit-learn` e `nltk`

Strumenti utilizzati

* **Python** (per scrivere il codice) mediante JupiterLab
* **Pandas & NumPy** (per gestire il dataset e pulire le righe duplicate)
* **NLTK** (per la manipolazione del testo: rimuovere parole inutili, fare lo stemming, ecc.)
* **Scikit-learn** (per trasformare il testo in vettori, addestrare il modello Naive Bayes e ottimizzare i parametri)
* **Joblib** (per salvare il modello pronto su disco senza doverlo riaddestrare ogni volta)

---

## Preprocessing

Prima di dare in pasto gli SMS al modello, il testo viene ripulito passo dopo passo:
* **Tutto in minuscolo:** Per far sì che "Free" e "free" vengano considerati la stessa parola.
* **Via i caratteri inutili:** Rimuove numeri e punteggiatura normale, tiene simboli importanti come `$` e `!` (molto frequenti nello spam).
* **Tokenizzazione:** Divide le frasi in liste di singole parole.
* **Rimozione Stop Words:** Elimina parole cortissime e poco informative come "and", "the", "is".
* **Stemming:** Riduce le parole alla loro radice (es. "running" e "runs" diventano entrambi "run") per raggruppare i concetti simili.
* **Ricostruzione stringa:** Riunisce le parole pulite in un'unica stringa.

A questo punto, si usa `CountVectorizer` per contare quante volte appaiono le parole singole (unigrammi) e le coppie di parole (bigrammi, come "free prize"), creando la matrice numerica per il modello.

.<img width="374" height="247" alt="risultato finale" src="https://github.com/user-attachments/assets/60edcd6d-4a52-410d-bfe4-261a5833be80" />


---

## Addestramento e Ottimizzazione

Per trovare la configurazione migliore per l'algoritmo `MultinomialNB`, ho usato `GridSearchCV` con una validazione incrociata (Cross-Validation). 
Ho cercato il valore migliore per il parametro **alpha** (che serve a gestire le parole totalmente nuove che il modello non ha mai visto prima) basandomi sul punteggio **F1-Score**, che è ottimo quando si gestiscono dataset in cui lo spam è molto meno frequente rispetto ai messaggi normali.

Infine, ho salvato il modello finale con "joblib". Quando l'applicazione viene riavviata o distribuita in un ambiente di produzione, il file viene ricaricato in memoria tramite `joblib.load()`. Il modello è immediatamente pronto per l'inferenza.
**Nota Informativa Importante:** Prima di passare i nuovi dati al modello caricato per la predizione, devono subire lo stesso identico preprocessing applicato ai dati di addestramento.


## Come provarlo
### Prerequisiti:
Installare le librerie necessarie: pip install pandas nltk scikit-learn joblib
## Esempio di utilizzo 
Una volta addestrato e salvato il modello, si può usare per testare nuove frasi al volo:

------------------------------------------------

import joblib

# Caricare il modello salvato
loaded_model = joblib.load('spam_detection_model.joblib')

# (Opzionale) Ricordarsi di passare il testo nella funzione di preprocessing prima!
new_messages = ["Congratulations! You've won a $1000 Walmart gift card."]
new_data_processed = [preprocess_message(msg) for msg in new_messages]

# Fare predizione
predictions = loaded_model.predict(new_data_processed)
print(predictions) # 1 se è spam, 0 se è ham

Ecco una proposta per il file `README.md` del tuo repository GitHub. È stato strutturato seguendo lo stile, il tono e la formattazione dell'esempio che hai fornito, integrando in modo fluido e organizzato tutti i progetti estratti dai file di testo.

---

---

## 2. CyberML Academy — Dashboard di Studio

Una vera e propria "bibbia" e dashboard personale sviluppata per visualizzare il mio curriculum di studio, tenere traccia dei progressi quotidiani e avere un accesso rapido agli strumenti operativi e alle guide completate.

<img width="938" height="826" alt="image" src="https://github.com/user-attachments/assets/36e668ce-9891-429c-a1fd-f1fdc745572a" />


### Strumenti utilizzati

* 
**HTML5 & CSS3:** Struttura della pagina e design "dark mode" (void/dark) con palette neon per ridurre l'affaticamento visivo durante le sessioni notturne.


* 
**Vanilla JavaScript:** Logica di rendering dinamico delle card, gestione delle animazioni e filtri delle guide.


* 
**Prompt Engineering (AI Co-creation):** Strutturazione logica, pianificazione e debug realizzati in sinergia con **Gemini** (struttura e debug JS), **Claude** (rifinitura CSS) e **Antigravity** (automazione script).



### Funzionalità principali

* 
**Curriculum Tracker:** Roadmap suddivisa in moduli per monitorare il completamento delle attività quotidiane con una *Progress Bar* visiva per i progressi settimanali.
<img width="869" height="418" alt="image" src="https://github.com/user-attachments/assets/e9a6571a-8d2b-48f3-bc4e-583bdb0d8a82" />


* 
**Arsenal:** Sezione dedicata alla collezione di tool e strumenti di sicurezza in fase di apprendimento.
<img width="920" height="926" alt="image" src="https://github.com/user-attachments/assets/eaada930-09d8-4e67-b772-4de1ba61705e" />


* 
**Guide dinamiche:** Sistema di card filtrabili per livello per consultare rapidamente appunti e tutorial.

<img width="1978" height="1190" alt="Senza titolo" src="https://github.com/user-attachments/assets/f28ead94-2714-481b-94fd-110edcf012fd" />
<img width="800" height="878" alt="image" src="https://github.com/user-attachments/assets/6ba7e8a1-3415-4bc5-b9a0-772a30d89757" />

<img width="908" height="865" alt="image" src="https://github.com/user-attachments/assets/271c624f-df8b-48bb-8b8e-bdc693a83d45" />

### Come usarlo

Essendo un progetto frontend statico, basta clonare il repository e aprire direttamente il file `index.html` nel browser (Chrome, Firefox, ecc.). Per aggiungere nuovi elementi, è sufficiente aggiornare gli array JavaScript o modificare il file HTML.

---

## 3. Network Anomaly Detection using Random Forest

Questo progetto affronta il problema dell'identificazione di attività malevole o intrusioni analizzando le caratteristiche del traffico di rete tramite un algoritmo di ensemble (**Random Forest**) basato su molteplici alberi decisionali.

### Strumenti utilizzati

* 
**Python 3** (per l'intera pipeline di sviluppo) 


* 
**Pandas & NumPy** (per il download, la manipolazione e il preprocessing del dataset) 


* 
**Scikit-Learn** (per il data splitting, l'addestramento del Random Forest e il calcolo delle metriche di valutazione) 


* 
**Seaborn & Matplotlib** (per la generazione di grafici e della heatmap per la Confusion Matrix) 


* 
**Joblib** (per il salvataggio e la persistenza del modello addestrato) 



### La Pipeline di Machine Learning

1. **Acquisizione Dati:** Download automatizzato ed estrazione locale dell'archivio `.zip` del dataset di riferimento **NSL-KDD** (standard di settore che elimina i record ridondanti e risolve lo sbilanciamento delle classi).


2. **Preprocessing & Data Transformation:** * Mappatura di oltre 40 colonne di feature di rete.


* Creazione di un target binario (`attack_flag`: 0 = normale, 1 = attacco).


* Creazione di un target multi-classe raggruppando decine di signature in 4 macro-categorie: **DoS** (1), **Probe** (2), **Privilege Escalation** (3) e **Access** (4).


* 
**One-Hot Encoding** delle variabili testuali (es. `protocol_type`) tramite `pd.get_dummies` e unione con le metriche numeriche.




3. **Data Splitting Strategico:** Per evitare il *data leakage* e l'overfitting, i dati sono divisi rigorosamente in: Core Training Set (fitting), Validation Set (tuning iperparametri) e un 20% di Test Set totalmente isolato per l'esame finale.


4. **Addestramento e Valutazione:** Allenamento del `RandomForestClassifier` e analisi dei risultati tramite accuratezza, Precision, Recall, F1-Score (fondamentali per le classi di attacco più rare) e matrice di confusione.



---

## Come provarli

### Prerequisiti

Per eseguire gli script Python e addestrare il modello di Network Anomaly Detection, installa le librerie necessarie:

```bash
pip install numpy pandas scikit-learn seaborn matplotlib joblib requests

```

### Esempio di utilizzo (Pipeline & Inferenza)

Di seguito viene mostrato l'estratto logico dei comandi per scaricare il dataset, addestrare il modello, valutarlo e infine salvarlo/ricaricarlo per i test:

```python
import requests, zipfile, io
import pandas as pd
import joblib
from sklearn.ensemble import RandomForestClassifier
from sklearn.metrics import classification_report

# 1. Download automatico del dataset
url = "https://academy.hackthebox.com/storage/modules/292/KDD_dataset.zip"
response = requests.get(url)
z = zipfile.ZipFile(io.BytesIO(response.content))
z.extractall('.')

# 2. Caricamento in Pandas
df = pd.read_csv('KDD+.txt', names=columns)

# 3. Addestramento del modello Random Forest (Multi-classe)
rf_model_multi = RandomForestClassifier(random_state=1337)
rf_model_multi.fit(multi_train_X, multi_train_y)

# 4. Valutazione delle Performance
multi_predictions = rf_model_multi.predict(multi_val_X)
print(classification_report(multi_val_y, multi_predictions, target_names=class_labels))

# 5. Esportazione e salvataggio locale
joblib.dump(rf_model_multi, 'network_anomaly_detection_model.joblib')

# 6. Caricamento futuro per inferenza immediata
# loaded_model = joblib.load('network_anomaly_detection_model.joblib')

```


