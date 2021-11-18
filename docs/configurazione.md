---
layout: default
title: Configurazione
nav_order: 2
---

# Configurazione
{: .no_toc }

## Indice
{: .no_toc .text-delta }

1. TOC
{:toc}

---

### Utilizzo repository e dipendenze

Monitoraggio vaccini Italia utilizza **[Python 3.7](https://docs.python.org/3.7/using/index.html)** per recuperare ed analizzare automaticamente i dati rilasciati nei [report settimanali](https://www.epicentro.iss.it/coronavirus/aggiornamenti) dell'Istituto Superiore di Sanità come ad es.:
<p align="center">
  <a href="https://www.epicentro.iss.it/coronavirus/bollettino/Bollettino-sorveglianza-integrata-COVID-19_10-novembre-2021.pdf">Bollettino-sorveglianza-integrata-COVID-19_10-novembre-2021.pdf</a>
</p>

1. Per cominciare clona il repository tramite il seguente comando:
```
git clone git@github.com:apalladi/covid_vaccini_monitoraggio.git
cd covid_vaccini_monitoraggio
```
2. Per contribuire al progetto è consigliata la creazione di un environment virtuale:
```
python -m venv .env
source .env/bin/activate
```
3. Nell'environment virtuale è possibile installare automaticamente i pacchetti richiesti utilizzando il seguendo comando:
```
pip install -r requirements.txt
```
4. Ti consigliamo di lavorare su una nuova branch cosi da permetterci eventuali cambiamenti:
```
git checkout -b [nome_nuovo_branch]
git push origin [nome_nuovo_branch]
```


### Utilizzo e spiegazione script

Lo script [**dati/dati_selezione.py**](https://github.com/apalladi/covid_vaccini_monitoraggio/blob/main/dati/dati_selezione.py) estrae i dati per l'analisi (tabella n.3) a partire dal report selezionato. I dati vengono salvati in [dati/dati_ISS_complessivi.csv](https://github.com/apalladi/covid_vaccini_monitoraggio/blob/main/dati/dati_ISS_complessivi.csv) e [dati/data_iss_età_YY-MM-D.csv](https://github.com/apalladi/covid_vaccini_monitoraggio/blob/main/dati/data_iss_età_2021-11-10.csv). Lo script è stato aggiornato il [10/11/2021](https://www.epicentro.iss.it/coronavirus/bollettino/Bollettino-sorveglianza-integrata-COVID-19_10-novembre-2021.pdf) per includere i vaccinati con dose aggiuntiva. Per i report precedenti a questa data utilizzare lo script [dati/dati_selezione_old.py](https://github.com/apalladi/covid_vaccini_monitoraggio/blob/main/dati/dati_selezione_old.py) e [dati/dati_ISS_complessivi_old.csv](https://github.com/apalladi/covid_vaccini_monitoraggio/blob/main/dati/dati_ISS_complessivi_old.csv).
Sono necessari ghostscript e tkinker per il corretto funzionamento di [camelot](https://camelot-py.readthedocs.io/en/master/user/install-deps.html).

I dati possono essere analizzati mediante i seguenti script:

1. [scripts/andamento_epidemia.py](https://github.com/apalladi/covid_vaccini_monitoraggio/blob/main/scripts/andamento_epidemia.py): calcola le curve epidemiche relative a nuovi casi, ospedalizzati, ricoverati in terapia intensiva e deceduti, divise per vaccinati e non vaccinati. Le curve epidemiche sono rapportate al numero di vaccinati e non vaccinati, in ogni intervallo temporale. In questo modo è possibile calcolare le incidenze (o tassi). Data la sproporzione tra il numero di vaccinati e non vaccinati, i numeri assoluti risultano infatti poco utili per monitare l'andamento dell'epidemia.

2. [scripts/andamento_rapporti_incidenze.py](https://github.com/apalladi/covid_vaccini_monitoraggio/blob/main/scripts/andamento_rapporti_incidenze.py): calcola il contributo dei non vaccinati rispetto all’incidenza totale nelle varie fasce di età.

3. [scripts/confronti_europei.py](https://github.com/apalladi/covid_vaccini_monitoraggio/blob/main/scripts/confronti_europei.py): aggiorna gli andamenti delle curve epidemiologiche e delle vaccinazioni dei paesi dell'Eurozona.

4. [scripts/confronto_2020_2021.py](https://github.com/apalladi/covid_vaccini_monitoraggio/blob/main/scripts/confronto_2020_2021.py): restituisce gli andamenti delle curve epidemiche 2020 e 2021. Per il 2021 vengono mostrate separatamente le curve dei vaccinati e dei non vaccinati.

5. [scripts/efficacia_vaccini.py](https://github.com/apalladi/covid_vaccini_monitoraggio/blob/main/scripts/efficacia_vaccini.py): calcola i tassi di contagio relativi all'ultimo report dell'ISS, dividendo i dati in 4 fasce d'età e in 2 categorie (vaccinati e non vaccinati). Ciò permette di calcolare le incidenze per ogni fascia d'età e di valutare correttamente l'efficacia dei vaccini nel prevenire il contagio, l'ospedalizzazione, il ricovero in terapia intensiva e il decesso.

Per eseguire un aggiornamento generale, utilizzare il seguente comando dalla directory principale:
```bash
./update_all.sh
```

