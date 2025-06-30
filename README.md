# manaproductionsgroup.github.io

# AI TOOLS NOTES

## NormalCrafter

https://github.com/Binyr/NormalCrafter

This tool generates NormalMap mappings. Not recommended for 12GB VRAM GPUs (although can run it if you downgrade the output), the minimum VRAM for 10 seconds of video at 30FPS is 20GB VRAM (tested in RunPod with RTX A2500).

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

