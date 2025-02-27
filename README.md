## TL;DR
* Clone Repository
* Download a [Keypoint File](https://drive.google.com/drive/folders/1hfLQhse5DP460Q-j0d-vG_obCVIsc9Bt?usp=sharing) (and if you want rename it to `hamer.safetensors`)
* Put `hamer.safetensors` into `<PATH_TO_REPOSITORY>/_DATA/hamer_ckpts/checkpoints/`
* Register and download MANO files [here](https://mano.is.tue.mpg.de/)
* Put the data from `mano_v1_2.zip` into `<PATH_TO_REPOSITORY>/_DATA/data`
* Use it with [hamer_keypoints](https://github.com/Schmetzler/hamer_keypoints.git)

# hamer_ckpt
The ~~checkpoint~~ config file for HaMeR.

This repository contains just the HaMeR ~~Checkpoint file and~~ config for HaMeR to use with [hamer_keypoints](https://github.com/Schmetzler/hamer_keypoints.git). 
I use [safetensors](https://github.com/huggingface/safetensors) to store the model weights. I extracted 3 Versions out of the original:

* **hamer.safetensors** The original float32 weights with just the discriminator thing removed (2.5GB)
* **hamer16.safetensors** The weights in bfloat16 format (but will be loaded as float32 so no speed improvement) (1.2GB)
* **hamer8.safetensors** The weights in float8_e4m3fn format (but will be loaded as float32 so no speed improvement) (0.6GB)

The original file was downloaded from https://www.cs.utexas.edu/~pavlakos/hamer/data/hamer_demo_data.tar.gz as in the original implementation of [HaMeR](https://github.com/geopavlakos/hamer.git) which also contains a model for VitPos, which is not needed for hamer_keypoint. I had to load the model and store it again as safetensors.

You should put the [MANO](https://mano.is.tue.mpg.de/) files under the data folder see the README.md of the data folder.

Clone the repository and set the path in hamer_keypoints like following:

```python
import hamer.configs
hamer.configs.CACHE_DIR_HAMER = "<PATH_TO_REPOSITORY>/_DATA"
from hamer.hamer_module import HAMER

# choose depending on your torch configuration
hamer = HAMER(device="cpu")
#hamer = HAMER(device="cuda")

# you can also load a different CHECKPOINT_FILE
# but it must have the 'model_config.yaml' 2 folders above
hamer = HAMER(device="cpu", checkpoint_path=f"{CACHE_DIR_HAMER}/hamer_ckpts/checkpoints/hamer8.safetensors")

# ... do stuff ... 
```

## Things are always a bit complicated

I tried with GitHub LFS but its still too big for my free tier... so I must resort to Google Drive (as everyone else does).

If my google drive space gets a little short I may remove the big file as you can resort to the [original file](https://www.cs.utexas.edu/~pavlakos/hamer/data/hamer_demo_data.tar.gz).

Load one file from [here](https://drive.google.com/drive/folders/1hfLQhse5DP460Q-j0d-vG_obCVIsc9Bt?usp=sharing).
Rename it and place it into `<PATH_TO_REPOSITORY>/_DATA/hamer_ckpts/checkpoints/hamer.safetensors`.

~~As I am only using GitHub Free the file size can only be 2 GB per file, so I had to split it into multiple files. It maybe necessary to install git-lfs to be able to pull the files.~~

~~So to use it just extract hamer.7z.001 (and obviously with hamer.7z.002) into the hamer_ckpts folder. It should extract to hamer.ckpt. You can remove the 7z files afterwards.~~

~~I don't want to use the google drive stuff, as I want the file to be available more consistently. And of course you would need 7zip to extract the file... have fun.~~
