# dvc
- https://dvc.org/doc/start

DVC - tutorial
# 1 - Handling Data
## Loading Data
- dvc get https://github.com/iterative/dataset-registry get-started/data.xml -o data/data.xml
- or
- dvc import https://github.com/iterative/dataset-registry get-started/data.xml -o data/data.xml
### Now one can do dvc update to bring in the changes from the data source later.

## Start Tracking
- dvc add data/data.xml
- git add data/data.xml.dvc data/.gitignore
- git commit -m "Add raw data"
- git push

# 2 - Cloud Storage
- dvc remote add -d storage drive://{gdrive link}
- git add .dvc/config
- git commit -m "Configure remote storage"
- dvc push

# 3 - Pipelines
### There are commands but I prefer adding directly to the dvc.yaml file.
## Reproducing Pipeline
-dvc repro

## Visualizing Pipeline
- dvc dag


# 4 - Metrics, Params, Plots
- dvc metrics show
- dvc plots show
- dvc params diff
- dvc metrics diff
- dvc plots diff


# 5 - Running an Experiment
## Set Param Value and Run the Experiment
- dvc exp run --set-param featurize.max_features=3000 
## See Differences
- dvc exp diff
## Queues experiments
- dvc exp run --queue -S train.min_split=8
- dvc exp run --queue -S train.min_split=64
- dvc exp run --queue -S train.min_split=2 -S train.n_est=100
- dvc exp run --queue -S train.min_split=8 -S train.n_est=50
- dvc exp run --queue -S train.min_split=64 -S train.n_est=200
## Run the Experiments in Parallel
- dvc exp run --run-all --jobs 2
## Show Experiments
- dvc exp show
## Shows Experiments/Filtered
- dvc exp show --no-timestamp --param-deps --sort-by avg_prec --only-changed
## Retrievable
- dvc exp apply exp-591af
## Show Experiments from 2 Commits ago
- dvc exp show -n 2
## Remove Experiments from Workspace
- dvc exp gc --workspace
