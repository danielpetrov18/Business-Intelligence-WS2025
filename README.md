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
# Some files and folders in the DPIM are omitted
.
├── DPIM
│   ├── evaluation_data    # Sources for individual event logs
│   ├── evaluation_results # Results of evaluation
│   └── main.py            # Implementation of DPIM
├── DPIM.pdf               # Paper
├── experiment.ipynb       # Recreation of the evaluation results in the paper
├── Evaluation Logs        # Event logs used for evaluation in the paper
├── README.md              # Summary and additional information
└── requirements.txt       # All dependencies for the project
```

#### A brief summary of the paper

Process discovery can leak sensitive information regarding a business process and entities involved in it. The worst case scenario is when every trace can be associated with a particular individual, leading to a high footprint.
The `Differentially Private Inductive Miner` or `DPIM` algorithm discussed in the paper proposes a new privacy-preserving method of building process trees (`PST`), while reducing data utility loss to a minimum. Instead of applying operations on individual traces, the `DPIM` does so on groups of traces. This approach assumes an attacker with authorization and suffiecient background knowledge able to perform a `difference attack`. At the heart of the `DPIM` lies the `differential privacy` or `DP` property that masks the influence of individual traces and outliers, by introducing a degree of noise. To ensure the generation of a faithful tree a rejection sampling is carried out during the algorithm.

#### Evaluation Logs

The paper makes use of 14 event logs 10 of which can be found under `https://data.4tu.nl/authors/acf80d21-bb77-4762-a219-2110947904b1`. The other 4 can be easily found on Google by entering their respective name. In this project all 14 event logs used for recreating the evaluation results are saved under `./Evaluation Logs` located in the root of the project. See `./DPIM/evaluation_data/BPI_Challenges.md` for more.

#### Replication

When trying to recreate the evaluation results of the paper one can use the `experiment` jupyter notebook found at the root of the project. The results are stored under `Evaluation_Results.xlsx`. **DO NOTE** that the evaluation experiments were performed on a fraction of the event logs - `10%` of each event log and for `BPI Challenge 2017.xes` only `1%`. Additionally, in the original evaluation results for computing the standard deviation and mean `n=100` is used, however in this experiment `n=10`. Due to taking samples one might need to re-run the notebook multiple times to compute all values. When sampling not all activities are considered - there's added non-determinism.
