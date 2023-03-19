# CandyRex-Song

config_path= 'location of config.yaml in the checkpoints archive'
# E.g.: './checkpoints/nyaru/config.yaml'
# The config and checkpoints are one-to-one correspondences. Please do not use other config files.

project_name='name of the current project'
# E.g.: 'nyaru'

model_path='full path to the ckpt file'
# E.g.: './checkpoints/nyaru/model_ckpt_steps_112000.ckpt'

hubert_gpu=True
# Whether or not to use GPU for HuBERT (a module in the model) during inference. It will not affect any other parts of the model.  
# The current version significantly reduces the GPU usage for inferencing the HuBERT module. As full inference can be made on a 1060 6G GPU, there is no need to turn it off.
# Also, auto-slice of long audio is now supported (both inference.ipynb and infer.py support this). Audio longer than 30 seconds will be automatically sliced at silences
