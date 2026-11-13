# Overflow metabolism in *E. coli* with flux balance analysis

A small learning project on acetate overflow in *E. coli*, using the core metabolic model and COBRApy.

**Author:** Pouria Johari, MSc student in Quantitative Biology, University of Milan

## The question

When *E. coli* grows fast, it secretes acetate even if oxygen is available. This looks wasteful, because respiration gives much more ATP per glucose than fermentation. Basan et al. (2015) explained it with protein cost: respiration needs more protein per ATP than fermentation, so a fast-growing cell with a limited amount of protein moves part of its energy production to fermentation.

In this project I check if a simple version of this idea works in a small metabolic model.

## What the notebook does

Everything is in `Overflow_Metabolism_FBA.ipynb`.

- **Part A: basic FBA.** Growth at different glucose uptake rates, growth without oxygen, and single gene knockouts to find the essential genes.
- **Part B: where basic FBA fails.** With oxygen available, the model never secretes acetate, at any growth rate.
- **Part C: a protein budget.** I add one constraint to the model: the protein used for respiration plus the protein used for growth cannot be more than a fixed budget. Then I repeat the glucose scan and compare it with basic FBA.

## Main results

- Basic FBA predicts full respiration and no acetate at every growth rate, which does not agree with real cells.
- With the protein budget, acetate secretion starts above a threshold growth rate and increases with growth rate. Oxygen uptake decreases after the same point. Both behaviours are seen in experiments.
- The switch to acetate appears for every respiration cost I tested, so it comes from the budget itself and not from one special parameter value.

## Limits

- The two cost values in the budget are chosen by hand and not measured. They set the growth rate where the switch happens (about 0.77 per hour with the values I used). So the model explains why overflow happens, but it does not predict when it starts in a real cell.
- Fermentation has no protein cost in this model, which is a simplification.
- The glucose scans stop at an uptake of 11.5 mmol/gDW/h. Above this value the optimal solution is not unique for acetate.
- The core model contains central metabolism only.

This is a simplified reproduction of a published idea and not a new result.

## How to run it

```
pip install cobra matplotlib numpy jupyterlab
jupyter lab
```

Open the notebook and choose Kernel > Restart Kernel and Run All Cells. It runs in less than a minute. Tested with Python 3.13.

## References

- Basan M, Hui S, Okano H, Zhang Z, Shen Y, Williamson JR, Hwa T. Overflow metabolism in *Escherichia coli* results from efficient proteome allocation. *Nature* 528, 99–104 (2015).
- Orth JD, Fleming RMT, Palsson BØ. Reconstruction and use of microbial metabolic networks: the core *Escherichia coli* metabolic model as an educational guide. *EcoSal Plus* (2010).
- Ebrahim A, Lerman JA, Palsson BO, Hyduke DR. COBRApy: COnstraints-Based Reconstruction and Analysis for Python. *BMC Systems Biology* 7, 74 (2013).

## Note

I used an AI assistant (Claude) as a tutor while learning COBRApy and for help with the code and the English.
