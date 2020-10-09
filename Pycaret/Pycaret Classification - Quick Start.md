# Pycaret Classification - Quick Start

## STEP 1: 설치

[Pycaret](https://pycaret.org/)
: Release: PyCaret 2.1 | Release Date: August 28, 2020

```bash
conda install -c conda-forge pycaret
```

## STEP 2: read_csv
```python
import pandas as pd

pd.set_option('max_columns', 500)
pd.set_option('max_rows', 500)

train = pd.read_csv(path + 'train.csv')
test = pd.read_csv(path + 'test_x.csv')
submission = pd.read_csv(path + 'sample_submission.csv')

df = train.copy()
```

# Classification Module

## STEP 3: Setting up Environment
```python
# #intialize the setup (in Notebook env)
from pycaret.classification import *
exp1 = setup(df, target = 'voted',
            ignore_features=['index'])
```

## STEP 4: Create Model
```python
# create_model(estimator = None, ensemble = False, method = None, fold = 10, round = 4, cross_validation = True, verbose = True, system = True, **kwargs)
lightgbm = create_model('lightgbm')=['index'])
```

## STEP 5: Tune Model
```python
# tune_model(estimator = None,  fold = 10,  round = 4,  n_iter = 10, custom_grid = None,  optimize = ‘Accuracy’, choose_better = False, verbose = True)
tuned_lightgbm = tune_model(lightgbm)
```

## STEP 6: Evaluate Model 
```python
# evaluate_model(estimator)
evaluate_model(tuned_lightgbm) 
```

## STEP 7: Predict Model
```python
# predict_model(estimator, data=None, probability_threshold=None, platform=None, authentication=None, verbose=True)
pred_holdouts = predict_model(lightgbm)
pred_holdouts.head()
```

## STEP 8: Finalize Model
```python
# finalize_model(estimator)
lightgbm_final = finalize_model(lightgbm)
predictions = predict_model(lightgbm_final, test)
```

## STEP 9: Submission - to_csv
```python
# to_csv
submission['voted'] = predictions['Score']
submission.to_csv('../output/submission_proba-Pycaret#02.csv', index = False)
```


## 참조
* [Pycaret Classification](https://pycaret.org/classification)
