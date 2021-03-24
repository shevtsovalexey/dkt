# Disease Knowledge Transfer across Neurodegenerative Diseases
Results replication of the original paper \[1] as a final project for the Machine Learning course at Skoltech.

Done by Team #14: Alexander Nevarko, Alexey Shevtsov, Maria Donskova, Konstantin Soshin.

The original public code release was done by the first author of the original paper Răzvan Marinescu at his [personal repository]( https://github.com/razvanmarinescu/dkt).

![overall diagram](disease_knowledge_transfer.png)


## Table of Contents
* [Requirements](#requirements)
* [Repository Structure](#repository-structure)
* [Results Reproduction](#results-reproduction)
* [References](#references)


## Requirements
- [Python](https://www.python.org) (v3.6 or later)
- [NumPy](http://numpy.org/) (v1.17.0 or later)
- [Pandas](https://pandas.pydata.org/) (v1.0.1 or later)
- [SciPy library](https://www.scipy.org/scipylib/index.html) (v0.19.0 or later)
- [Matplotlib](https://pypi.org/project/matplotlib/) (v.3.2.0 or later)


## Repository Structure
```
├── tadpoleDrc.py                                           # main file
├── data_processed
│   ├── tadDrcTiny.npz
│   └── validDf.csv                                          
│
├── drcRes.html                                             # joint table with the results
│
├── resfiles                                                # detailed experiment results
│   ├── synth                                                   # synthetic data experiment
│   │   ├── synth1_JMD     
│   │   │   ├── init                                                    # initialization
│   │   │   ├── fitRes{iter}{step}.npz                                  # checkpoints
│   │   │   ├── compTrueParams{iter}{step}_synth1_JMD.png               # synthetic biomarkers estimation (agnostic)
│   │   │   ├── trajDisSpaceDis0{iter}{step}_synth1_JMD.png             # synthetic biomarkers estimation (AD)
│   │   │   ├── trajDisSpaceDis1{iter}{step}_synth1_JMD.png             # synthetic biomarkers estimation (PCA)
│   │   │   └── plotHierData{iter}{step}_synth1_JMD.png                 # optimization steps visualization
│   │   └── synth1.npz                                              # fitted model
│   │
│   ├── tadDrcTiny_JMD                                          # DKT [1] experiment
│   │   ├── init                                                    # initialization
│   │   ├── fitRes{iter}{step}.npz                                  # checkpoints
│   │   ├── plotHierData{iter}{step}_tadDrcTiny_JMD.png             # optimization steps visualization
│   │   ├── trajDisSpace{disease}{iter}{step}_tadDrcTiny_JMD.png    # optimization steps visualization
│   │   └── trajDisSpaceOverlap_{disease}_tadDrcTiny_JMD.png        # biomarker estimation for the AD or PCA disease  
│   │                                    
│   └── tadDrcTiny_Sig                                          # Latent stage [2] experiment
│       ├── allTraj{iter}{step}_tadDrcTiny_Sig.png                  # optimization steps visualization
│       └── fittedGPModel.npz                                       # fitted model
│
├── ...                                                    # auxiliary files
└── README.md
```


## Results reproduction

### Real data
To reproduce the results with ADNI + DRC data from pre-trained models run:
```
python3 tadpoleDrc.py --runIndex 0 --agg 1 --nrProc 10 --modelToRun 0 --nrRows 4 --nrCols 6 --penalty 5 --runPartStd LL --tinyData
```


To reproduce the results with ADNI + DRC data after training models form scratch run:

```
python3 tadpoleDrc.py --runIndex 0 --agg 1 --nrProc 10 --modelToRun 0 --nrRows 4 --nrCols 6 --penalty 5 --runPartStd LR --tinyData
```
The optimization steps for DKT [1] and Latent space [2] models are visualized with the `*.png` plots during training inside the corresponding folder with the experiment. 


### Synthetic data
To reproduce the results with synthetic data run:

```
python3 jointSynth.py --runIndex 0 --agg 1 --nrProc 10 --modelToRun 14 --nrRows 3 --nrCols 4 --runPartStd LL --expName synth1
```

## References
[1] Marinescu, Răzvan V., et al. "Disease knowledge transfer across neurodegenerative diseases." International Conference on Medical Image Computing and Computer-Assisted Intervention. Springer, Cham, 2019

[2] Jedynak, Bruno M., et al. "A computational neurodegenerative disease progression score: method and results with the Alzheimer's disease neuroimaging initiative cohort." Neuroimage 63.3 (2012): 1478-1486.
