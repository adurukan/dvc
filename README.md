# dvc
- https://dvc.org/doc/start

DVC - tutorial
# Handling Data
- dvc get https://github.com/iterative/dataset-registry get-started/data.xml -o data/data.xml
## a better alternative
- dvc import https://github.com/iterative/dataset-registry get-started/data.xml -o data/data.xml
## Now one can do dvc update to bring in the changes from the data source later.
## Loads the data from the link
- dvc add data/data.xml
## Start tracking
- git add data/data.xml.dvc data/.gitignore
- git commit -m "Add raw data"
- git push
## Track with git
- dvc remote add -d storage drive://{gdrive link}
- git add .dvc/config
- git commit -m "Configure remote storage"
## added a cloud storage
- dvc push
## Pushed to track with dvc and also data is pushed

# Pipelines
There are commands but I prefer adding directly to the dvc.yaml file.
-dvc repro
## The whole point of creating this dvc.yaml file is the ability to easily reproduce a pipeline. dvc repro relies on the DAG definition from dvc.yaml, and uses dvc.lock to determine what exactly needs to be run.
- dvc dag
## Helps visualizin the pipeline






# Running an Experiment
- dvc exp run --set-param featurize.max_features=3000 
## Sets the values for max_features, updates in params.yaml
- dvc exp diff
## Returns the difference in experiments
- dvc exp run --queue -S train.min_split=8
- dvc exp run --queue -S train.min_split=64
- dvc exp run --queue -S train.min_split=2 -S train.n_est=100
- dvc exp run --queue -S train.min_split=8 -S train.n_est=50
- dvc exp run --queue -S train.min_split=64 -S train.n_est=200
## Queues experiments
- dvc exp run --run-all --jobs 2
## Runs all of the experiments in parallel
- dvc exp show
## Shows an extensive table
- dvc exp show --no-timestamp --param-deps --sort-by avg_prec --only-changed
## Only shows the changed params and sorted by avg_prec
- dvc exp apply exp-591af
## Similar to dvc checkout but works with experiments, lets us retrieve it later.
- dvc exp show -n 2
## Shows the experiments from two commits ago.
- dvc exp gc --workspace
## Removed experiments from workspace