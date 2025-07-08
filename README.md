# Multicollinearity Resolution – DPR Framework Codebase

This repository contains the **data & MATLAB code** that powered the paper
“*Multicollinearity Resolution Based on Machine Learning: A Case Study of Carbon Emissions*,”
which won **First Prize** in the Chinese National Undergraduate Statistics Modeling Competition (全国大学生统计建模大赛). The DPR (DBSCAN + Penalised Regression) workflow tackles **high-dimensional, highly correlated drivers** of carbon emissions:

1. **DBSCAN** clusters 46 industries into objectively determined categories.
2. **Elastic Net** inside each cluster selects the most informative yet non-redundant variables, resolving multicollinearity.
3. **GM(1,1)** grey-prediction and **AR(q)** models forecast future emissions per cluster.
4. Diagnostic plots (ROC, NROC, confusion matrices) assess classification and prediction quality.([arxiv.org][1])

```text
Multicollinearity_Resolution
│
├── origin_data/          # raw industry-level carbon-emission tables (2000-2019)
├── processed_data/       # DBSCAN-clustered & scaled feature sets
│
├── step1_classify.mlx    # DBSCAN clustering + PCA visual-check
├── step2_data.mat        # intermediate feature matrix after scaling / clean-up
├── step3_identify.mat    # Elastic-Net coefficients & kept features
├── step4_predict.m       # GM(1,1) & AR(q) forecasting scripts
├── step5_pic.m           # ROC / PR / confusion-matrix plotting
├── step6_chart.m         # dashboard-style composite chart builder
│
├── matlab.zip            # one-click archive of *all* .mlx/.m code
└── paper_figures/        # ROC.png, NROC2.png, confusion matrices, etc.
```

---

## Quick Start (MATLAB R2020b + Statistics & ML Toolbox)

```matlab
% 0.  Clone the repo and unzip matlab.zip (or use the .m/.mlx files directly).

% 1.  Unsupervised clustering & category labelling
open step1_classify.mlx       % runs DBSCAN → saves cluster labels

% 2.  Elastic-Net variable screening (auto-executes inside the live script)
%     └── output: step3_identify.mat  (β, λ, retained features)

% 3.  Time-series forecasting for each DBSCAN category
run step4_predict.m           % GM(1,1) & AR(q) multi-step forecasts

% 4.  Visual diagnostics
run step5_pic.m               % ROC / PR curves
run step6_chart.m             % composite dashboard for the report
```

> **Tip:** `step4_predict.m` contains several *ready-made* vectors (`A`) so you can
> replicate every cluster’s forecast by uncommenting the line you need. It also
> includes built-in **Q-test**, **C-ratio**, and **P-probability** checks for GM(1,1) accuracy.([raw.githubusercontent.com][2])

---

## Repository Layout

| Folder / file        | Role                                                  |
| -------------------- | ----------------------------------------------------- |
| `origin_data/`       | Raw 46-industry energy & emission records (CSV / XLS) |
| `processed_data/`    | Cleaned, normalised, DBSCAN-labelled datasets         |
| `step1_classify.mlx` | DBSCAN + PCA explorer, exports label vector           |
| `step2_data.mat`     | MATLAB struct of scaled features & labels             |
| `step3_identify.mat` | Elastic-Net β-matrix, λ path, VIF stats               |
| `step4_predict.m`    | GM(1,1) single-series & AR(q) multi-series forecaster |
| `step5_pic.m`        | Generates ROC, NROC and confusion-matrix PNGs         |
| `step6_chart.m`      | Assembles all figures for the final report            |
| `matlab.zip`         | Convenience bundle with every script / figure         |
| `paper_figures/`     | High-resolution figures used in the arXiv draft       |

---

## Results Snapshot

* **16 distinct clusters** covering 93 % of variance in the 2000-2019 dataset.
* Elastic-Net reduced > 300 raw indicators to **38 non-collinear drivers**.
* GM(1,1) forecasts achieve **mean absolute percentage error (MAPE) ≤ 3 %** on
  20-year back-tests (Cluster 1 example shown in `ROC3.png`).([raw.githubusercontent.com][3])

---

## Citing

```bibtex
@article{zhang2025multicollinearity,
  title={Multicollinearity Resolution Based on Machine Learning: A Case Study of Carbon Emissions in Sichuan Province},
  author={Zhang, Xuanming},
  journal={arXiv preprint arXiv:2507.02912},
  year={2025}
}
```

---

## License

Released under the **Apache 2.0** License. See `LICENSE` for details.

---

## Acknowledgements

* Competition Committee of the National Undergraduate Statistics Modeling Contest.
* MATLAB *Statistics & Machine Learning Toolbox* for clustering and Elastic-Net, and *Econometrics Toolbox* for AR-model functions.
* The open-source community for inspirational multicollinearity-handling examples.

Happy analysing!

[1]: https://arxiv.org/abs/2507.02912 "[2507.02912] Multicollinearity Resolution Based on Machine Learning: A Case Study of Carbon Emissions"
[2]: https://raw.githubusercontent.com/XMZhangAI/Multicollinearity_Resolution/main/step4_predict.m "raw.githubusercontent.com"
[3]: https://raw.githubusercontent.com/XMZhangAI/Multicollinearity_Resolution/main/README.md "raw.githubusercontent.com"
[4]: https://github.com/XMZhangAI/Multicollinearity_Resolution "GitHub - XMZhangAI/Multicollinearity_Resolution: 全国大学生统计建模大赛一等奖"
