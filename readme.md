
# Natural-Language to Pandas with LLMs  

---

## Project Overview
This repository demonstrates an end-to-end workflow in which a Large Language Model (LLM) converts plain-English analytical questions into executable **Pandas** code.  
Key points:

* **Dataset** UCI Household Power Consumption (Dec-2006 → Nov-2010, 2 M rows).  
* **Model** `qwen-qwq-32b` served through the **Groq** API.  
* **Safety** Generated code runs in an isolated namespace with `df.copy(deep=True)` so the master DataFrame is never mutated.  

---

## Repository Layout
```

├── llm_queries.ipynb                     # Jupyter notebook (main pipeline)                     
└── README.md                             # /power-llm.git
 
 
```

### 2 · Provide your Groq API key
```
export GROQ_API_KEY="sk-xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
```


## Notebook Walk-Through
| Step | Purpose |
|-----:|---------|
| 1 | Load the raw text file → parse dates → create a `DateTimeIndex`. |
| 2 | Define seven benchmark questions + reference Pandas solutions. |
| 3 | Build a strict **system prompt** demanding pure code in triple back-ticks. |
| 4 | Call Groq → Llama-3 to get code for each question. |
| 5 | **Sandbox exec:** run code in a namespace containing only `df.copy(deep=True)` and std-lib. |

---


---

## ⚙️ Dependencies
* Python 3.11
* pandas ≥ 2.2
* matplotlib ≥ 3.9
* groq ≥ 0.7
* jupyterlab / notebook  

Full, pinned versions live in `environment.yml`.

 
