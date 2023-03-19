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
wav_fn='xxx.wav'  
# The path to the input audio. The default path is in the project's root directory.

use_crepe=True  
# CREPE is an F0 extraction algorithm. It has good performance but is slow. Changing this to False will use the slightly inferior but much faster Parselmouth algorithm.

thre=0.05  
# CREPE's noise filtering threshold. It can be increased if the input audio is clean, but if the input audio is noisy, keep this value or decrease it. This parameter will have no effect if the previous parameter is set to False.

pndm_speedup=20  
# Inference acceleration multiplier. The default number of diffusion steps is 1000, so changing this value to 10 means synthesizing in 100 steps. The default, 20, is a moderate value. This value can go up to 50x (synthesizing in 20 steps) without obvious loss in quality, but any higher may result in a significant quality loss. Note: if use_gt_mel below is enabled, make sure this value is lower than add_noise_step. This value should also be divisible by the number of diffusion steps.

key=0
# Transpose parameter. The default value is 0 (NOT 1!!). The pitch from the input audio will be shifted by {key} semitones, then synthesized. For example, to change a male voice to a female voice, this value can be set to 8 or 12, etc. (12 is to shift a whole octave up).

use_pe=True
# F0 extraction algorithm for synthesizing audio from the Mel spectrogram. Changing this to False will use the input audio's F0.
# There is a slight difference in results between using True and False. Usually, setting it to True is better, but not always. It has almost no effect on the synthesizing speed. 
# (Regardless of what the value of the key parameter is, this value is always changeable and does not affect it)
# This function is not supported in 44.1kHz models and will be turned off automatically. Leaving it on will not cause any errors as well.

use_gt_mel=False
# This option is similar to the image-to-image function in AI painting. If set to True, the output audio will be a mix of the input and target speaker's voices, with the mix ratio determined by the parameter below.
# NOTE!!!: If this parameter is set to true, make sure the key parameter is set to 0 since transposing is not supported here.

add_noise_step=500
# Related to the previous parameter, it controls the ratio of the input and target voice. A value of 1 will be entirely the input voice, and a value of 1000 will be entirely the target voice. A value of around 300 will result in a roughly equal mixture of the two. (This value is not linear; if this parameter is set to a very low value, you can lower pndm_speedup for higher synthesis quality)


wav_gen='yyy.wav'
# The path to the output audio. The default is in the project's root directory. The file type can be changed by changing the file extension here. 

pip install -r requirements_short.txt
