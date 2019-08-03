# Install_tensorflow_jetson_nano_Cpp_lib
# Steps to build TensorFlow v1.12.0 C-library on Jetson Nano for GPU

* Thank Saurabh Deoras for help

## Jetson Nano configuration
* ARM 64 (aarch64)
* gcc 7.3
* cuda 10
* cudnn 7

## TensorFlow configuration
* v1.12.0
* v1.13.1 could not be built (see: https://github.com/tensorflow/tensorflow/issues/27931 )

## Steps
* Enable at least 6GB swap space per: https://www.jetsonhacks.com/2019/04/14/jetson-nano-use-more-memory/
* Build bazel 0.18 from source. Newer bazel versions may have issues.
* Checkout `v1.12.0` from tensorflow github repo
* Apply diff shown below (tf_jetson_nano_build_112.diff). This was derived from https://github.com/tensorflow/tensorflow/issues/21852#issuecomment-477885516
* Configure build using command `./configure` from within the TF folder.
* Set GPU capability value to 5.3 and disable NCCL when possible or choose a value of 1.3
* Answer `No` whenever possible except of-course yes to cuda support.
* Cuda is installed at default location, however location for cudnn should be `/usr`
* Start build using command: `nohup bazel build --config=cuda --config=noaws //tensorflow:libtensorflow.so &`
* Patience...
* After several hours you should see `libtensorflow.so` and `libtensorflow_framework.so` files in `bazel-bin` folder
