# Bird migration energetics: simulation code and data

Code, data and figures for the preprint

**Energy Landscapes, Stopover Networks and Reproductive Constraints: A Mathematical Framework for Arctic–European Bird Migration under Climate Change**
Valeria Ciurcina, ORCID [0000-0001-8184-2901](https://orcid.org/0000-0001-8184-2901)

A simulation of a generic goose-type bird (about 2 kg) migrating north through a network of eight stopover wetlands to a breeding site. It tracks fat, route choice, arrival time and calcium, and turns the result into a population growth rate (lambda). Seven scenarios test how wind, earlier springs, habitat loss and calcium-poor staging change migration success and reproduction, alone and combined.

## What is in this repository
| Path | Content |
|---|---|
| `sim.py` | The model: flight, stopover, route choice, reproduction, Leslie matrix, the 7 scenarios |
| `figs.py` | Runs all scenarios and draws figures 1–5 (about 2–3 minutes) |
| `exp2.py` | Extra experiments for figure 6 (fitness vs departure date; calcium uptake) |
| `tests.py` | Six sanity tests |
| `summ.json`, `grids.json`, `add.json`, `exp2.json` | Result files |
| `figs/` | The six figures (PNG) |
| `R_package/` | R translation (`sim.R`, `run_scenarios.R`), `README_R.md` and all data as CSV in `R_package/data/` |

## Run the Python version
```
pip install numpy scipy matplotlib
python3 tests.py
python3 figs.py
```
Random seeds are fixed, so results reproduce exactly.

## Run the R version
```r
setwd("R_package")
source("run_scenarios.R")
```
Base R only. For a quick trial set `N <- 500` in `run_scenarios.R`. R uses a different random-number stream, so results agree with the Python version statistically, not digit by digit. The R code is a translation of `sim.py` and has not yet been run by the author; see `R_package/README_R.md`.

## Expected key results (Python, 4,000 birds per scenario)
| Scenario | Arrival probability | Reproductive index | Lambda |
|---|---|---|---|
| Baseline | 0.992 | 0.909 | 1.000 |
| A. Weaker tailwind | 0.980 | 0.789 | 0.980 |
| B. Earlier food and thaw | 0.981 | 0.888 | 0.988 |
| C. B plus earlier departure | 0.991 | 0.951 | 1.003 |
| D. Western wetlands degrade | 0.979 | 0.846 | 0.984 |
| E. Calcium-poor staging | 0.992 | 0.732 | 0.987 |
| F. A + B + D combined | 0.791 | 0.531 | 0.782 |

## Important
All parameters are assumptions for a generic bird, not estimates from data. Potential fecundity is calibrated so that the baseline growth rate equals 1, so only differences between scenarios are meaningful. Scenarios are sensitivity tests, not climate projections.

## Where to change things
- Bird traits and timing: dictionary `P` at the top of `sim.py` (or `R_package/data/parameters.csv` for R)
- Sites (position, habitat quality, calcium uptake): list `NODES` (or `R_package/data/nodes.csv`)
- Scenarios: list `SC` at the bottom of `sim.py`

## License
Code: MIT (see `LICENSE`). Figures and text: CC BY 4.0.
