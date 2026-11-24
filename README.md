# Lightweight Cybersickness Detection based on User-Specific Eye and Head Tracking Data in Virtual Reality

Code for the paper by Yijun Wang, Mihai Bâce and Maria Torres Vega (KU Leuven), submitted to *Virtual Reality* (Springer).

The paper detects the current cybersickness (CS) level (None, Low, Medium, High) from windows of about 3 s of
eye-tracking and head-tracking data recorded by the built-in sensors of a head-mounted display. Its main method,
incremental personalization, adapts an XGBoost model trained on other users to each target user with the user's
own Fast Motion Sickness Score (FMS) reports, evaluated under a chronological test-then-train protocol.

## Repository structure

```
├── data/                          # not included, see data/README.md
├── model_comparison/
│   ├── ml_models.ipynb            # SVM-RBF, Random Forest, XGBoost, Extra Trees, Stacking-Tree
│   ├── dl_models.ipynb            # LSTM, GRU, CNN-LSTM, TD-CNN-LSTM, DeepTCN, ALSTM-FCN
│   └── statistical_tests.ipynb    # Friedman test, Wilcoxon signed-rank tests with Holm correction, 95% CIs
├── feature_selection/
│   └── feature_selection.ipynb
├── data_levels/
│   └── data_levels.ipynb
├── incremental/
│   └── incremental_personalization.ipynb
└── LICENSE
```

## Data

The experiments use the *Simulation 2021* dataset. The raw data are not included in this repository.
Access to the raw data has to be requested from the authors of:

> Islam, R., Desai, K., Quarles, J. (2021). Cybersickness Prediction from Integrated HMD's Sensors: A Multimodal
> Deep Fusion Approach using Eye-tracking and Head-tracking Data. IEEE International Symposium on Mixed and
> Augmented Reality (ISMAR).

`data/README.md` describes the two preprocessed files that the notebooks expect.

## Environment

The incremental personalization experiments were run with Python 3.14.3, XGBoost 3.2.0 (2 threads),
scikit-learn 1.8.0, imbalanced-learn 0.14.1, pandas 3.0.1 and NumPy 2.4.3.

```
pip install numpy==2.4.3 pandas==3.0.1 scikit-learn==1.8.0 imbalanced-learn==0.14.1 xgboost==3.2.0 scipy==1.17.1 matplotlib==3.10.8 jupyter
```

`dl_models.ipynb` additionally needs TensorFlow, which may require an older Python version than 3.14.

All experiments use the random seed 42.

## Citation

The citation will be added after publication.

## License

This code is released under the MIT License (see `LICENSE`).
