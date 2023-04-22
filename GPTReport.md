
[elisaromondia.it](https://www.elisaromondia.it) 

<sub>Aggiornato *(21.04.2023)*</sub>


<sub>*[Versioni precedenti](https://gist.github.com/elicatinthebox/b93c3930e603e39beedf72b82604f1ef)*</sub>

### GPT Open AI 

------

#### Costi [source](https://openai.com/pricing)
Il costo del servizio viene calcolato per 1,000 token. Token sono intesi come porzioni di testo. 1,000 token equivalgono circa a 750 parole. E' possibile utilizzare un tool online chiamato "Tokenizer" per capire come specifiche porzioni di testo vengono tokenizzate: [Tokenizer](https://platform.openai.com/tokenizer)

**GPT-4**: Sulla base di un'ampia conoscenza di base su differenti domini, l'utima versione di GPT (GPT 4) può seguire istruzioni complesse in linguaggio naturale e risolvere problemi difficili con precisione. [source](https://openai.com/product/gpt-4)

| Model  | Prompt  |  Completion |
|---|---|---|
| 8K context	| $0.03 / 1K tokens | $0.06 / 1K tokens | 
| 32K context	| $0.06 / 1K tokens | $0.12 / 1K tokens |   


**Fine-tuning models**: E' possibile personalizzare la conoscenza di base dei modelli su campioni di dati specifici utilizzando la tecnica del fine tuning fino a creare modelli custom.  

| Model  | Training  |  Usage |
|---|---|---|
| Davinci	| $0.0300 / 1K tokens | $0.1200 / 1K tokens | 


------

#### Scalabilità

Come dichiarato nella pagina del princing di OpenAI, è ad oggi possibile iniziare una fase di *sperimentazione con un credito gratuito di $5 per i primi 3 mesi*. 

La sperimentazione consente di valutare quale modello meglio si adatta alle esigenze del progetto dando la possibilità di testare i differenti modelli con relative capacità e costi. Dopo la prova è previsto un pagamento calcolato sull'uso effettivo delle risorse *(pay as you go)*.


------ 

#### Approfondimento: Fine tuning

I modelli di GPT sono pre-addestrati su una grande quantità di testo disponibile in quello che viene definito "internet aperto". Quando viene fornito un prompt con pochi esempi, spesso può intuire quale attività si sta tentando di eseguire e generare un completamento plausibile (apprendimento detto "few-shot learning"). 

Il fine-tuning è una tecnica che consente di creare modelli custom aderenti a specifici casi d'uso. Questa tecnica migliora l'apprendimento detto "few-shot learning" allenando il modello su molti più esempi di quelli che possono essere inseriti nel prompt, consentendo di ottenere risultati migliori su un ampio numero di attività. In sintesi: 

 > * Risposte di qualità superiori poiché basati su set di dati specifici e non generali
 > * Capacità di allenare il modello su più esempi di quelli che possono stare in un prompt
 > * Una volta che un modello è stato messo a punto, non sarà più necessario fornire esempi nel prompt
 > * Risparmio di risorse, minor numero di token grazie alla possibilità di  prompt ridotti
 > * Richieste più veloci (minore latenza)



Per modelli specializzati, l'applicazione del fine-tuning segue tre momenti: 

 > 1. Preparare e caricare i set di dati per il training del modello
 > 2. Addestramento del nuovo modello custom
 > 3. Fine-tuned model pronto all'uso


------

#### Approfondimento: set di dati per l'addestramento

I dati devono essere nel formato [JSONL document](https://jsonlines.org/), dove *ogni riga è una coppia **prompt-completamento** corrispondente a un esempio di addestramento*. Attualmente OpenAI fornisce un tool chiamato [CLI data preparation tool](https://platform.openai.com/docs/guides/fine-tuning/cli-data-preparation-tool) per facilitare la conversione dei dati nel formato richiesto (JSONL).

Open AI suggerisce per completare il fine tuning di un modello di fornire una serie di dati di addestramento composta da *almeno alcune centinaia* di esempi di addestramento costituiti ciascuno da *un singolo input **("prompt")** e dall'output associato **("completamento")**.* Linearmente con ogni raddoppio del numero di esempi, le prestazioni tendono ad aumentare. Aumentare il numero di esempi è di solito il modo migliore e più affidabile per migliorare le prestazioni.


------

#### Casi d'uso
1. **Esempio di fine tuning classification [Notebook](https://github.com/openai/openai-cookbook/blob/main/examples/Fine-tuned_classification.ipynb)**. Modello in grado di classificare se una parte di testo di input è correlata al Baseball o all' Hockey.


2. **Esempio di fine-tuning model specialized for Q&A [Notebook](https://github.com/openai/openai-cookbook/blob/main/examples/fine-tuned_qa/olympics-3-train-qa.ipynb)** In questo notebook viene usato un set di dati composto da coppie di contesto (Q&A), per creare ulteriori domande contraddittorie e coppie di contesto, in cui la domanda non è stata generata in quel contesto. In questi casi al modello verrà richiesto di rispondere "Nessun contesto sufficiente per rispondere alla domanda". In questo notebook è possibile esplorare l'addestramento anche di anche un modello "discriminatore", che prevede se è possibile rispondere o meno alla domanda sulla base del contesto.

*Numerosi altri esempi di utlizzo sono esplorabili dalla pagina dedicata di OpenAI : [Examples Applications](https://platform.openai.com/examples)*


