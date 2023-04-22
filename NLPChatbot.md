# NLP Chatbot

[elisaromondia.it](https://www.elisaromondia.it/)

<sub>Aggiornato *(22.04.2023)*</sub>


---
## **La scelta del modello**

Per la progettazione di NLP Chatbot che possa interagire in lettura con un database è necessario capire quale sia il livello di “feeling umano” che si vuole ottenere, per questo è necessaria una scelta fra i livelli di complessità di un **modello NLP (natural language processing)**:

 * natural language understanding (NLU)	
 * natural language generation (NLG) 



La comprensione del linguaggio naturale è necessaria al processamento, per tanto, un modello NLP sarà sempre anche NLU. Tuttavia, non tutti i modelli NLP sono capaci di generare linguaggio naturale, se si desidera questa abilità è necessario valutare un modello che sia anche generativo quindi, un NLP che sia NLU+NLG.

<sub>***Per approfondire: [IBM](https://www.ibm.com/blog/nlp-vs-nlu-vs-nlg-the-differences-between-three-natural-language-processing-concepts/), [Wikipedia](https://en.wikipedia.org/wiki/Natural_language_generation#Example)***</sub>


Ad oggi, un chatbot NLP che includa il processo generativo (NLG) è quanto di più vicino alla sensazione di conversare con un essere umano. 

Secondo l’esigenza di poter interrogare un db e fornire una risposta all’utente che interagisce con il chatbot, un chatbot di questo tipo è ad oggi la soluzione che consente la maggiore possibilità di interpretare una domanda scritta in linguaggio naturale, tradurla in forma di codice, interagire con il db, trasformare l'output ricevuto e generare una risposta all’utente in linguaggio naturale.

Questo risultato è ottenibile di base con modelli come [GPT 3.5](https://platform.openai.com/docs/models/gpt-3-5) o [GPT 4](https://platform.openai.com/docs/models/gpt-4) senza necessità di fine tuning, poiché già "addestrati" a questa abilità.

<sub>***Per approfondire: [querying data using Azure AI](https://medium.com/microsoftazure/querying-structured-data-with-azure-openai-e59ee43867e5), [infoq](https://www.infoq.com/news/2023/03/azure-openai-chatgpt-preview/), [codex](https://openai.com/blog/openai-codex)***</sub>

È possibile interrogare un db con un chatbot NLP non generativo ma per farlo è necessario insegnare al chatbot dei dialoghi specifici che siano quanto più vicini alle domande che potrebbe fare un utente. Questo richiede più risorse in termini di tempo e costi poiché prevede un addestramento per questo compito specifico. Quanto lungo in termini di tempo dipende dalla quantità e dalla complessità delle interazioni (inteso come dialoghi e flussi) che si desidera insegnare al chatbot.

***Esempio**: In questo [video](https://www.instagram.com/tv/B2yyM8Xh4ZV/?igshid=YmMyMTA2M2Y=) è possibile visionare un esperimento condotto da me e [Lorenzo Zaccagnini](https://lorenzozaccagnini.it/) per l’implementazione di Dialog Flow nel [progetto open source devoleum](https://www.devoleum.com/) e la sua integrazione con l’assistente vocale Google Home. In questo esperimento abbiamo addestrato un chatbot NLP (senza integrazione di modelli generativi) su  dialoghi specifici legati all’interazione con i dati delle storie delle filiere pubblicate su devoleum. Abbiamo integrato poi la possibilità di interagire con il chatbot tramite l’assistente vocale Google Home.*

L’uso di un modello NLP non generativo presenta il vantaggio rispetto a modelli generativi di poter essere sì più limitato (meno creativo) nella capacità di “conversare” ma anche più aderente rispetto alle istruzioni, evitando così di produrre le cosiddette risposte “allucinate” prodotte dai Large Language Model (LLM), come ad esempio GPT 3. 

<sub>***Per approfondire: [Hallucination (artificial intelligence) wikipedia](https://en.wikipedia.org/wiki/Hallucination_(artificial_intelligence)), [Large Language Model (LLM) wikipedia](https://en.wikipedia.org/wiki/Large_language_model)***</sub>



---
## **Sperimentazione in locale**

È possibile a scopo sperimentale, la prova in locale sia di modelli generativi che di modelli NLP base, tuttavia, nel primo caso è ad oggi possibile solo con modelli che hanno capacità ridotte rispetto a modelli come GPT4. Secondo la mia esperienza per la sperimentazione in locale le opzioni migliori sono:

**Chatbot NLP non generativi:**


* **[Microsoft Bot Framework Composer](https://github.com/microsoft/BotFramework-Composer/blob/main/README.md)** *(in questo caso Microsoft predispone la possibilità di implementare opzionalmente anche un NLP generativo).*
* **[ProjectAna](https://github.com/nowfloats/ProjectAna)**
* **[Tock][https://doc.tock.ai/tock/en/](https://github.com/theopenconversationkit/tock)**

Tutte le soluzioni elencate sono open source, sperimentabili in locale, con la possibilità di usufruire di un'interfaccia grafica che consente di creare un chatbot e testestarlo senza la necessità di scrivere codice. Per l’integrazione con un database è possibile il test in locale ma è necessaria la capacità di gestione di API e server per poter far comunicare il chatbot con il db desiderato.

**Chatbot NLP generativi:**


* **[oobabooga](https://github.com/oobabooga/text-generation-webui) + [llama.cpp](https://github.com/ggerganov/llama.cpp#usage)**

Oobabooga è una gradio web UI che consente l’esecuzione di LLM come LLaMA, llama.cpp, GPT-J, ovvero i maggiori modelli attualmente disponibili per uso sperimentale. 

Il secondo di questi llama.cpp è una versione ottimizzata del modello[ LLaMa realizzato da Meta AI](https://research.facebook.com/publications/llama-open-and-efficient-foundation-language-models/). Questa ottimizzazione ha consentito di abbassare il consumo di risorse per l’esecuzione in locale. Da notare che per garantire questa ottimizzazione anche le capacità conversazionali del modello sono state ridotte.

Nel primo caso il tempo di sperimentazione dipende dalla complessità e dalla quantità di dialoghi che si desidera insegnare al chatbot, nel secondo caso la sperimentazione in locale richiede la potenza di calcolo della macchina su cui si vuole sperimentare che influisce anche sulla tempistica con cui è possibile interagire con il modello per la sperimentazione. Nella mia esperienza, per un uso accettabile da pc è consigliabile una configurazione con una scheda video Nvidia RTX 2060 o superiore. 

Questo per un modello generativo limitato come llama.ccp, tuttavia è possibile testare anche modelli più performanti ma questo aumenta la richiesta di capacità delle macchine su cui testarlo. Come potrebbe aumentare i tempi di esecuzione. Nella mia esperienza, la metodologia migliore è quella di procedere gradualmente al fine di trovare il compromesso più aderente al risultato che si desidera. Valutando bene se investire per la sperimentazione di modelli complessi in un ambiente locale. 

<sub>***Per approfondire:  [Running dolly2 locally](https://huggingface.co/databricks/dolly-v2-12b/discussions/27)***</sub>

Da notare che progetti open source e/o disponibili ad uso gratuito, hanno il vantaggio di non avere costi per l’uso degli stessi in sperimentazione ma non significa che non abbiano vincoli di licenze. Inoltre, chi mantiene vivo ad oggi il progetto può decidere domani di non renderlo più pubblico e non non ne garantisce la funzionalità nel tempo. Il rischio di investire risorse in strumenti che non possono garantire una continuità è elevato ed il mio consiglio è di valutare una sperimentazione di questo tipo solo in una fase esplorativa.

Per un eventuale fine tuning, che è la fase più critica e costosa in termini di risorse, il mio consiglio è quello di affidarsi a servizi cloud cercando di ridurre così al minimo il rischio di bruciare risorse.


---
## **Esempi di soluzioni per uso commerciale**

* **Servizi AI Cloud:**

  * **Google Cloud: [AI di conversazione naturale con agenti virtuali all'avanguardia. Disponibile in due versioni: Dialogflow CX (avanzata) e Dialogflow ES (standard). ](https://cloud.google.com/dialogflow?hl=it)**
  * **Azure AI: [Bot e agenti virtuali intelligenti](https://powervirtualagents.microsoft.com/it-it/)**
  * **AWS:  [Building AI chatbots using Amazon Lex and Amazon Kendra](https://aws.amazon.com/it/blogs/machine-learning/building-ai-chatbots-using-amazon-lex-and-amazon-kendra-for-filtering-query-results-based-on-user-context/)**


  Per tutte e tre le soluzioni AI Cloud è possibile una vasta configurazione che consente l’implementazione dei modelli AI (generativi e non) e modelli macchina più performanti ad oggi disponibili. Nella mia esperienza per una soluzione commerciale di un chatbot NPL che possa interagire con db in tempo reale l’utilizzo di servizi cloud è la scelta più funzionale che consente anche la possibilità di svolgere una fase sperimentale altamente configurabile secondo le proprie esigenze. 


* **Soluzioni Custom:** Non è esclusa la possibilità di realizzare delle soluzioni custom da zero, tuttavia è una via complessa che sconsiglio per la richiesta esosa di risorse, specialmente se si vuole realizzare anche un LLM, sia in termini di professionisti che di macchine. Costi e tempistiche anche in questo caso sono estremamente variabili e dipendono dalle caratteristiche del chatbot NLP che si desidera realizzare. Per questo, nella mia esperienza, è consigliabile condurre almeno la sperimentazione avvelendosi di servizi AI Cloud che possano monitorare l’utilizzo delle risorse in modo dettagliato al fine di pianificare lo sviluppo di una soluzione custom con una possibile pianificazione dei costi avvalendosi di un team di sviluppo esperto nella realizzazione di NLP chatbot custom. 
