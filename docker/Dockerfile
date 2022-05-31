FROM nvcr.io/nvidia/pytorch:21.10-py3

ARG DEBIAN_FRONTEND=noninteractive
RUN apt update
RUN apt install ffmpeg libsm6 libxext6 git -y
RUN apt clean
RUN rm -rf /var/lib/apt/lists/*

# remove NVIDIA's nofig...
RUN rm /opt/conda/etc/jupyter/jupyter_notebook_config.py

# Torch - Torchvision - IceVision - IceData - MMDetection - YOLOv5 - EfficientDet Installation
RUN wget https://raw.githubusercontent.com/airctic/icevision/master/icevision_install.sh

# Choose your installation target: cuda11 or cuda10 or cpu
RUN bash icevision_install.sh cuda11 master

# install other dependencies
RUN pip install python-gdcm
RUN pip install pydicom
RUN pip install pynrrd
RUN pip install slicerio
RUN pip install ipywidgets

EXPOSE 8889

ENTRYPOINT ["jupyter", "notebook", "--allow-root", "--port=8889", "--ip=0.0.0.0", "--no-browser", "--NotebookApp.token=''"]
