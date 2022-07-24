# dvc
DVC - tutorial










# Running an Experiment
- dvc exp run --set-param featurize.max_features=3000 
## Sets the values for max_features, updates in params.yaml
- dvc exp diff
## Returns the difference in experiments
- dvc exp run --queue -S train.min_split=8
- dvc exp run --queue -S train.min_split=64
- dvc exp run --queue -S train.min_split=2 -S train.n_est=100
- dvc exp run --queue -S train.min_split=8 -S train.n_est=100
- dvc exp run --queue -S train.min_split=64 -S train.n_est=100
## Queues experiments
- dvc exp run --run-all --jobs 2
## Runs all of the experiments in parallel