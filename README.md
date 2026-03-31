# manaproductionsgroup.github.io

# TOOLS

## ESSENTIAL FFMPEG COMMANDS

### Convert video to frames
`ffmpeg -r 1 -i video.mp4 -r 1 "%03d.jpg"`

### Convert frames to video
`ffmpeg -framerate 8 -pattern_type glob -i '*.jpg' -c:v copy output.mp4`

### Reverse a video
`ffmpeg -i output.mp4 -vf reverse -af areverse output_rev.mp4`

# AI TOOLS NOTES

Keep in mind you have to install CUDA Toolkit version 12, and set in the bash `export CUDA_HOME=/usr/local/cuda-12` so it can compile the binaries with CUDA 12 on RTX 50xx/CUDA 13.0 system in case CUDA 12 is necessary.

## Hunyuan3D 2.1 (ComfyUI)

clone ComfyUI repo, enter to the folder and:

IMPORTANT: use `pip install torch==2.7.0 torchvision==0.22.0 torchaudio==2.7.0 --index-url https://download.pytorch.org/whl/cu128` instead if you have an RTX 50xx for this.

```
python3.11 -m venv .venv
source .venv/bin/activate
pip install torch==2.5.1 torchvision==0.20.1 torchaudio==2.5.1 --index-url https://download.pytorch.org/whl/cu124
pip install -r requirements.txt
cd custom_nodes
git clone https://github.com/visualbruno/ComfyUI-Hunyuan3d-2-1.git
cd ComfyUI-Hunyuan3d-2-1
pip install -r requirements.txt
cd hy3dpaint/custom_rasterizer
python3 setup.py install
cd ../DifferentiableRenderer
python3 setup.py install
cd ../..
pip install transformers==4.49 diffusers==0.32.2 rembg onnxruntime # downgrade and adding more missing dependencies
git clone https://github.com/SarahWeiii/diso.git # adding a dependency where only works with compiling it locally
cd diso
python3 setup.py install
cd ../..
python3 main.py --lowvram
```

## bgbye

git clone https://github.com/MangoLion/bgbye

and edit `server/setup.sh` replacing the same paragraph with this one:
```
# Install Python dependencies
pip install numpy==1.26.4 #WEIRD IMPORT ERROR WORKAROUND FOR REMBG
pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu128
pip install fastapi uvicorn transformers pillow scikit-image transparent-background rembg opencv-python-headless python-multipart requests
pip install carvekit #--extra-index-url https://download.pytorch.org/whl/cu121
pip install onnxruntime #ADDED TO FIX ModuleNotFoundError
```

and follow the same installation/run steps shown in the repo.

## NormalCrafter

https://github.com/Binyr/NormalCrafter

This tool generates NormalMap images from videos. Not recommended for 12GB VRAM GPUs (although can run it if you downgrade the output), the minimum VRAM for 10 seconds of video at 30FPS and 1024 image size of output is 20GB VRAM (tested in RunPod with RTX A2500).

The original repo has no instructions *what you should install* to run correctly but here you have it:

```py
### IN RUNPOD YOU SHOULD USE PYTORCH 2.1 (CUDA 11.8)
sudo apt-get install ffmpeg # in case you're running in RunPod
pip install torch==2.0.1+cu117 torchvision==0.15.2+cu117 torchaudio==2.0.2 --index-url https://download.pytorch.org/whl/cu117 # correct torch versions

### Then follow the normal instructions
# Use python3.10 venv in case if applies, in RunPod is not needed

git clone https://github.com/Binyr/NormalCrafter
cd NormalCrafter
pip install -r requirements.txt
python3 app.py
```

