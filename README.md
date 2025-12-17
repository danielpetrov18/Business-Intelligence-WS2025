# Business Intelligence WS2025

## Group Project

### Members

* Markschies Benjamin Max a12133418
* Daniel Petrov a12028482
* Fallah Mohammad Mahdi a01428941
* Jargalsaikhan Solongo a01348898
* Watholowitsch Alexander a11911292

#### Prerequisite

```bash
# 1.) Create a virtual environment
python3 -m venv venv

# 2.) Activate it
source venv/bin/activate

# 3.) Install dependencies
python3 -m pip install -r requirements.txt
```

#### Project structure

```bash
.
├── DPIM                  # The practical project that implements the paper 
├── DPIM.pdf              # Differentially Private Inductive Miner paper
├── eval_experiment.ipynb # Recreation of the evaluation in the paper
├── Evaluation Logs       # Event logs used for evaluation in the paper
├── README.md             # Summary and additional information
└── requirements.txt      # All dependencies for the project
```

#### Evaluation Logs

The paper makes use of 14 event logs 10 of which can be found under `https://data.4tu.nl/authors/acf80d21-bb77-4762-a219-2110947904b1`. The other 4 can be easily found on Google by entering their respective name.

#### How to run

When trying to recreate the evaluation results of the paper one can perform the following command in the terminal for individual event logs:

```bash
# Note that event logs need to be uncompressed first.
python3 DPIM/main.py "Evaluation Logs/<event log>" -t 0.95 -e 0.01 -l <varies> -u <varies>
```

The threshold `t` is always `0.95` and the epsilon `e` always `0.01` for all experiments. The lower and upper bounds vary based on the event log used. To find that information go to `DPIM/README.md`.
