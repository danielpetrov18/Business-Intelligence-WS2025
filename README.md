# Business Intelligence WS2025

## Group Project

### Members

* Markschies Benjamin Max a12133418
* Petrov Daniel a12028482
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
│   ├── evaluation_data     # Sources for individual event logs
│   ├── evaluation_results  # Results of evaluation (from the paper)
│   └── main.py             # Implementation of DPIM
├── DPIM.pdf                # Paper
├── experiment.ipynb        # Recreation of the evaluation results in the paper
├── Evaluation_Results.xlsx # Recreated evaluation results (group project)
├── Evaluation Logs         # Event logs used for evaluation in the paper
├── README.md               # Summary and additional information
└── requirements.txt        # All dependencies for the project
```

#### System used for replication

This project was developed and tested on the following system:

* **OS**: EndeavourOS x86_64
* **CPU**: 11th Gen Intel i7-11370H (8) @ 3.300GHz
* **RAM**: 16GB DDR4
* **GPU**: NVIDIA GeForce RTX 3060 with 8GB VRAM

#### A brief summary of the paper

Process discovery can leak sensitive information regarding a business process and entities involved in it. The worst case scenario is when every trace can be associated with a particular individual, leading to a high footprint.
The `Differentially Private Inductive Miner` or `DPIM` algorithm discussed in the paper proposes a new privacy-preserving method of building process trees (`PST`), while reducing data utility loss to a minimum. Instead of applying operations on individual traces, the `DPIM` does so on groups of traces. This approach assumes an attacker with authorization and suffiecient background knowledge able to perform a `difference attack`. At the heart of the `DPIM` lies the `differential privacy` or `DP` property that masks the influence of individual traces and outliers, by introducing a degree of noise. To ensure the generation of a faithful tree a rejection sampling is carried out during the algorithm.

#### Evaluation Logs

The paper makes use of 14 event logs 10 of which can be found under `https://data.4tu.nl/authors/acf80d21-bb77-4762-a219-2110947904b1`. The other 4 can be easily found on Google by entering their respective name. In this project all 14 event logs used for recreating the evaluation results are saved under `./Evaluation Logs` located in the root of the project. See `./DPIM/evaluation_data/BPI_Challenges.md` for more.

#### Replication

For recreating the evaluation results of the paper one can use the `experiment` notebook found at the root of the project. The results are stored under `Evaluation_Results.xlsx`.
**DO NOTE** that the evaluation experiments were performed on a fraction of the event logs - `10%` of each event log and for `BPI Challenge 2017.xes` only `1%`. Additionally, in the original evaluation results for computing the standard deviation and mean `n=100` is used, however in this experiment `n=10`. Due to taking samples one might need to re-run the notebook multiple times to compute all values due to some process trees being rejected for being unfaithful (having low fitness). When sampling not all activities are considered - there's added non-determinism.

##### Inductive Miner via PM4Py vs Differentially Private Inductive Miner (no privacy)

The authors of the paper conclude the following results - most of the metrics fall in the range of $\pm$ `10%` of the respective IM values.

During the replication the following conclusions have been made:

* `fitness` in both cases is assumed to be `100%` or `1`.
* `precision` tends to experience higher deviations in some cases than reported in the original paper reaching `22%`.
* `simplicity` falls exactly in the ranges discussed in the paper and it turns out to be the most stable metric.
* `generalization` also respects the boundaries proposed in the paper with the exception of the event logs `DomesticDeclarations` (`12%`) and `BPI_Challenge_2013_incidents` (`14%`) deviation.

##### Inductive Miner via PM4Py vs Differentially Private Inductive Miner (with privacy)

`fitness`:

* $\epsilon$=3:
Very similar results can be reported as the ones discovered in the paper. Most cases fall in the range of `95%` with 2 of the event logs having a fitness of `90%` - `BPIC15_3` and `RequestForPayment`.

* $\epsilon$=1
As epsilon is reduced more noise needs to be introduced. However, the event logs have very similar values with the exception of `RequestForPayment` which is off by `12%`.

* $\epsilon$=0.1
Similar results can be observed, but in some instances fitness is reduced quite drastically - for both
`BPI_Challenge_2013_closed_problems` and `BPI_Challenge_2013_open_problems` by `12%`.

* `precisions`:
The authors observe an increase in the precision for almost all the privacy degrees (epsilon values), however in this experiment the inverse is true. Most values are equal or below the ones produced by the Inductive Miner via PM4Py. There's also a tendency in this experiment for the `precision` to go down as the privacy increases ($\epsilon$ goes down) which seems counter-intuitive. A plausible reason for this odd behavior might be how data is randomly sampled and also due to the fact that for computing the mean values 10 iterations are performed instead of 100 `(n=10)`.

* `simplicity`:
In some cases the initial value goes up and some rarer cases it goes down. Generally `simplicity` remains quite stable just as observed in the paper. Just like in the paper `PrepaidTravelCosts` and `BPI_Challenge_2013_open_problems` experience a slight growth as the privacy increases and in our conducted experiments the same trend also for `InternationalDeclarations` and `BPI_Challenge_2013_closed_problems`.

* `generalization`:
Similar results can be observed in our experiments compared to the ones reported in the paper. Initially, the generalization goes down for almost all event logs and as the privacy increases the `generalization` either reduces or it stagnates.

#### Contributions

* Markschies Benjamin Max a12133418 - **Presentation Slides + Presentation**
* Petrov Daniel a12028482 - **Replication**
* Fallah Mohammad Mahdi a01428941 - **Additional Investigation**
* Jargalsaikhan Solongo a01348898 - **Presentation Slides**
* Watholowitsch Alexander a11911292 - **Additional Investigation**
