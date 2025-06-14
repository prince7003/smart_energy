```markdown
# Natural-Language to Pandas with LLMs  
_Auto-generating, sandbox-executing & verifying code on the UCI “Individual Household Power Consumption” dataset_

---

## Project Overview
This repository demonstrates an end-to-end workflow in which a Large Language Model (LLM) converts plain-English analytical questions into executable **Pandas** code.  
Key points:

* **Dataset** UCI Household Power Consumption (Dec-2006 → Nov-2010, 2 M rows).  
* **Model** `llama3-8b-instruct` served through the **Groq** API.  
* **Safety** Generated code runs in an isolated namespace with `df.copy(deep=True)` so the master DataFrame is never mutated.  
* **Verification** Each LLM answer is compared against a ground-truth snippet; results are displayed in a score table.

---

## Repository Layout
```

|── household_power_consumption.txt   # raw UCI text file 127 MB
├── llm_queries.ipynb                     # Jupyter notebook (main pipeline)
├── helper.py                             # Groq wrapper + secure exec helpers
├── environment.yml                       # Conda environment (Python 3.11)
└── README.md                             # /power-llm.git
cd power-llm

# create and activate the exact environment
conda env create -f environment.yml
conda activate energy-llm
```

### 2 · Provide your Groq API key
```
export GROQ_API_KEY="sk-xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
```

### 3 · Run the notebook
```
jupyter lab          # or: jupyter notebook
# open `llm_queries.ipynb` and Run ▶ all cells
```
A results table will appear; the `is_match` column should read **True** for every row.

---

## 📝 Notebook Walk-Through
| Step | Purpose |
|-----:|---------|
| 1 | Load the raw text file → parse dates → create a `DateTimeIndex`. |
| 2 | Define seven benchmark questions + reference Pandas solutions. |
| 3 | Build a strict **system prompt** demanding pure code in triple back-ticks. |
| 4 | Call Groq → Llama-3 to get code for each question. |
| 5 | **Sandbox exec:** run code in a namespace containing only `df.copy(deep=True)` and std-lib. |
| 6 | Compare model output with ground truth → tabulate accuracy. |

---
 

---
 

## 📊 Extending the Benchmark
Add more Q&A pairs in the `SOLUTIONS` dict inside the notebook.  
The evaluation cells automatically pick them up and add rows to the score table.

---

## ⚙️ Dependencies
* Python 3.11
* pandas ≥ 2.2
* matplotlib ≥ 3.9
* groq ≥ 0.7
* jupyterlab / notebook  

Full, pinned versions live in `environment.yml`.

 