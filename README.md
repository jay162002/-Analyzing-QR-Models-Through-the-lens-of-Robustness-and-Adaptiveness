# Analyzing QR Models: Through the lens of Robustness and Adaptiveness

> ⚠️ **Research Paper in Progress:**
> I am currently in the process of writing a **research paper** of this work.
> To maintain originality and avoid plagiarism or copy issues before publication, **the full implementation code will be made public after the paper is published**


This project studies and explores different popular **quantile estimation** methods and check how they performs in the presence of outliers.

Are they Robust and Adaptive at a same time?

proposes a new approach — **Trimmed Pinball Loss (TPL)** — that achieves both **robustness** and **adaptivity** in the presence of outliers.


### Quantile Estimation Methods 
- Pinball Loss Quantile Regression  
- Model Agnostic Quantile Regression (**MAQR**)  
- Tube Loss Quantile Regression  
- Orthogonal Quantile Regression (**OQR**)  

Through experiments on both **synthetic** and **real-world benchmark datasets**, we demonstrate that **TPL** achieves consistent improvements in robustness and adaptivity.


## Research Goals
- Analyze how existing QR methods behave under varying levels of outliers.  
- Evaluate adaptivity and Robustness across multiple quantile levels.  
- Propose and validate **Trimmed Pinball Loss (TPL)** 
- Demonstrate TPL’s Robustness and Adaptiveness using both **synthetic** and **UCI benchmark datasets**.


### 1️⃣ Synthetic Dataset
- **Samples:** 1000 points  
- **Outlier ratios:** 2%, 5%, and 10% contamination  

### 2️⃣ Real-World Datasets
- **Benchmark datasets:** Boston Housing, Concrete, Energy, Kin8nm, Naval, and Yacht  
- **Metrics:**  
  - **Expected Calibration Error (ECE)** — measures quantile calibration  
  - **RMSE** between clean and outlier-affected predictions — measures robustness



## Results

### 🧪 Synthetic Data (10% Outliers)
| Quantile (τ) | Pinball RMSE | Trimmed Pinball RMSE | MAQR RMSE |
|:--|:--:|:--:|:--:|
| 0.010 | 3.674 | **0.285** | 0.659 |
| 0.025 | 2.284 | 0.436 | **0.245** |
| 0.050 | 0.434 | **0.340** | 0.215 |
| 0.900 | 0.278 | **0.148** | 0.650 |
| 0.975 | 1.742 | **0.236** | 0.460 |
| 0.990 | 3.579 | **0.374** | 0.712 |

**Observation:** TPL consistently lowers RMSE, especially for extreme quantiles


### Influence of Outlier Percentage (Synthetic)
| Outlier % | Method | Average RMSE (τ=0.01–0.99) |
|:--|:--|:--:|
| 2% | Pinball: 0.35 | MAQR: 0.24 |
| 5% | Pinball: 0.59 | MAQR: 0.42 |
| 10% | **Trimmed Pinball: 0.30 (lowest)** | — |


### Boston Housing Dataset
| Method | ECE (Clean) | ECE (With Outliers) | RMSE (Clean vs Outlier) |
|:--|:--:|:--:|:--:|
| Pinball | 0.0155 | 0.0355 | 6.6559 |
| MAQR | 0.0069 | 0.0199 | 3.0123 |
| **Trimmed Pinball** | — | **0.0171** | **2.2446** |


### UCI Benchmark Results (All Attributes)
| Dataset | Pinball RMSE | Trimmed RMSE | MAQR RMSE |
|:--|:--:|:--:|:--:|
| Boston | 6.97 | **2.54** | 4.75 |
| Concrete | 10.50 | **4.79** | 7.60 |
| Energy | 12.80 | **6.11** | **5.44** |
| Kin8nm | 0.32 | **0.12** | 0.21 |
| Naval | 0.010 | **0.010** | 0.011 |
| Yacht | 14.89 | **3.16** | 10.49 |

