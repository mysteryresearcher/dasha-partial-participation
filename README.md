This repository provides the code to reproduce the experiments of the submission for Thirty-sixth Conference on Neural Information Processing Systems (NeurIPS 2022)

## Quick Start
### 1. Install [Singularity](https://sylabs.io/guides/3.5/user-guide/introduction.html) (optional)
If you don't want to install Singularity, make sure that you have all dependecies from Singularity.def (python3, numpy, pytorch, etc.)

a. Pull an image 
````
singularity pull library://k3nfalt/default/python_ml:sha256.efcd1fc038228cb7eb0f6f1942dfbaa439cd95d6463015b83ceb2dbaad9e1e98
````
b. Open a shell console of the image
````
singularity shell --nv ~/python_ml_sha256.efcd1fc038228cb7eb0f6f1942dfbaa439cd95d6463015b83ceb2dbaad9e1e98.sif
````
### 2. Prepare scripts for experiments
````
PYTHONPATH=./code python3 ./code/distributed_optimization_library/experiments/dasha_partial_participation/config_libsvm_dasha_partial_particiaption.py 
--dumps_path SOME_PATH --dataset_path PATH_TO_FOLDER_WITH_DATASET --dataset real-sim 
--experiments_name EXPERIMENT_NAME 
--num_nodes_list 100 --step_size_range -10 0 --number_of_seeds 1 --number_of_iterations 5000000 
--algorithm_names zero_marina_sync_stochastic zero_marina_partial_participation_stochastic --cpus_per_task 11 
--number_of_processes 10 --time 10 --parallel --compressors rand_k --number_of_coordinates 200 --quality_check_rate 1000 
--oracle stochastic --mega_batch 10000 --batch_size 1 --function stochastic_logistic_regression --logistic_regression_nonconvex 0.001 
--partial_participation_probabilities 1.0 0.5 0.1 0.01
````
### 3. Execute scripts
````
sh SOME_PATH/EXPERIMENT_NAME/singularity_*.sh
````
### 4. Plot results
````
PYTHONPATH=./code python3 ./code/distributed_optimization_library/experiments/plots/dasha_partial_participation/plot_vr-marina_real-sim_stochastic.py 
--dumps_paths SOME_PATH/EXPERIMENT_NAME 
--output_path SOME_PATH_FOR_PLOTS 
--ignore_methods "VR-MARINA (online)" "DASHA-MVR"
````

One can find all other scripts [here](https://github.com/mysteryresearcher/dasha-partial-participation/blob/submission_neurips2022/code/distributed_optimization_library/experiments/plots/dasha_partial_participation/script.txt) that generate experiments from the paper.
