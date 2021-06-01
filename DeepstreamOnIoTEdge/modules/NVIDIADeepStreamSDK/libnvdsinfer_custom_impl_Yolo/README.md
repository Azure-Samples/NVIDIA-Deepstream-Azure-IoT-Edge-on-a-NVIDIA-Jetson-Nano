# How to compile the libnvdsinfer_custom_impl_Yolo for your version of DeepStream

To parse the bounding boxes found by the object detection models from Microsoft Custom Vision's service with NVIDIA DeepStream, one needs to write a dedicated plugin. This is because Microsoft Custom Vision's service uses a tiny YOLO v2 model as the baseline for their compact object detection models. DeepStream needs to be calibrated with the same parameters as the ones used by Microsoft Custom Visions's service in order for DeepStream to properly understand the bounding boxes's coordinates. This parametrization can be done by follow steps similar to [these instructions](https://docs.nvidia.com/metropolis/deepstream/dev-guide/text/DS_custom_YOLO.html). The parametrization has already been done in this sample but one needs to compile the libnvdsinfer_custom_impl_Yolo to match exactly their CUDA and TensorRT versions. This document describes the steps required to compile this library on a jetson device.

## Install DeepStream on the host

Install the same version of DeepStream has the one installed in the container that you want to use directly on the host of your Jetson Device. For instance, for DeepStream 5.1, follow [these instructions](https://docs.nvidia.com/metropolis/deepstream/dev-guide/text/DS_Quickstart.html).

## Download and compile the updated nvdsparsebbox_Yolo.cpp

Download the `nvdsparsebbox_Yolo.cpp` and `Makefile` from the `libnvdsinfer_custom_impl_Yolo` in this repo and replace these files from the DeepStream installation above. In the case of DeepStream 5.1, these files are located in this folder `/opt/nvidia/deepstream/deepstream-5.1/sources/objectDetector_Yolo/nvdsinfer_custom_impl_Yolo`.

Compile this library by running `sudo CUDA_VER=xx.x make` where xx.x is your CUDA version, for instance 10.2 in the case of DeepStream 5.1.

## Use the newly compiled library in your solution
Follow the instructions in the main README with your newly compiled `libnvdsinfer_custom_impl_Yolo.so` library.