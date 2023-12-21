[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/rkroshan/anomalib_intel/blob/main/notebooks/pcb_anomaly_detection/collab_pcb_anamalib_detection.ipynb)

# About this notebook
- This notebook is taken a lot of reference from 000_getting_started notebook.
- This notebook trains a pcb anomaly detection model (here we are trying to detect solder shorts), then inference it via openvino (which is fast :))
- This PCB is a simple STM32 microcontroller board which I developed long back
- I used MvTEc dataset format (train, test and ground_truth directories) and update config.yaml. You can have custom dataset model as well refering notebook datamodels
- If you want to have you own PCB image for training make share good and training should have very minor differences (except anomaly, ofcourse). The alignment and orientation should be similar. Else you will not get good results for anamoly segmentation. Although model can detect good and bad pcb images without alignment and orientation issues

## How training works
- All images are truncates and center crop to 1024x1024 dimension. (Although there is a feature for center crop in config.yaml I didn't tries that)
- I tried model PADIM and updated its config.yaml to get pcb dataset
- Since images are large, I gave `image_size: 768` and turn on tiling with `tile_size: 256` and `stride: 256` . You can refer to tiling in notebook datamodels
- You can try with `image_size: 1024` as well but google_colab crashes since consuming lot of ram :(
- After training completes you can get an model.onxx in results directly which you can also save for later
- You can simply start from `OpenVINO Inference` if you have your model ready to know the anamoly on you test image.