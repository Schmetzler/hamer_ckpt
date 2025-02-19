# hamer_ckpt
The ~~checkpoint~~ config file for HaMeR ~~(which is 2.6GB in size !!!)~~.

This repository contains just the HaMeR ~~Checkpoint file and~~ config for HaMeR to use with [hamer_keypoint](https://github.com/Schmetzler/hamer_keypoint.git). It is the CPU version of the model so it should be able to load, even if the GPU has less memory. I had to load it in a CPU only torch environment and save it again. I think it can be transferred to the GPU after loading.

The original file was downloaded from https://www.cs.utexas.edu/~pavlakos/hamer/data/hamer_demo_data.tar.gz as in the original implementation of [HaMeR](https://github.com/geopavlakos/hamer.git) which also contains a model for VitPos, which is not needed for hamer_keypoint.

Just for reference I converted it this way:

```python
from lightning import Trainer
trainer = Trainer(enable_checkpointing = False)
from hamer.hamer_module import HAMER
# be aware you have to use a CPU only torch environment when using the original ckpt file
hamer = HAMER(device="cpu")
trainer.strategy._lightning_module = hamer.model
trainer.save_checkpoint("hamer.ckpt")
```

You should put the MANO files under the data folder see the README.md of the data folder.

Clone the repository and set the path in hamer_keypoints like following:

```python
import hamer.configs
hamer.configs.CACHE_DIR_HAMER = "<PATH_TO_REPOSITORY>/_DATA"
from hamer.hamer_module import HAMER

# choose depending on your torch configuration
hamer = HAMER(device="cpu")
#hamer = HAMER(device="cuda")

# ... do stuff ... 
```

## Things are always a bit complicated

I tried with GitHub LFS but its still too big for my free tier... so I must resort to Google Drive (as everyone else does).
The file is [here](https://drive.google.com/file/d/1Hnl04nIlRUhnJsKEKcHQY0qBqXhzpmgS/view?usp=sharing).
It is called `hamer.ckpt` and must be placed into `<PATH_TO_REPOSITORY>/_DATA/hamer_ckpts/checkpoints/hamer.ckpt`.

~~As I am only using GitHub Free the file size can only be 2 GB per file, so I had to split it into multiple files. It maybe necessary to install git-lfs to be able to pull the files.~~

~~So to use it just extract hamer.7z.001 (and obviously with hamer.7z.002) into the hamer_ckpts folder. It should extract to hamer.ckpt. You can remove the 7z files afterwards.~~

~~I don't want to use the google drive stuff, as I want the file to be available more consistently. And of course you would need 7zip to extract the file... have fun.~~
