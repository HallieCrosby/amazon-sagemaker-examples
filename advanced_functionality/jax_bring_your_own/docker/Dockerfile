# Copyright 2021 Amazon.com, Inc. or its affiliates. All Rights Reserved.
#
# Licensed under the Apache License, Version 2.0 (the "License"). You
# may not use this file except in compliance with the License. A copy of
# the License is located at
#
#     http://aws.amazon.com/apache2.0/
#
# or in the "license" file accompanying this file. This file is
# distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF
# ANY KIND, either express or implied. See the License for the specific
# language governing permissions and limitations under the License.

# Dockerfile for training models using JAX
# We build from NVIDIA container so that CUDA is available for GPU acceleration should the AWS instance support it
FROM nvidia/cuda:11.1-cudnn8-devel-ubuntu18.04

# Install python3
RUN apt update && apt install -y python3-pip

RUN ln -sf /usr/bin/python3 /usr/bin/python && \
    ln -sf /usr/bin/pip3 /usr/bin/pip

RUN pip --no-cache-dir install --upgrade pip setuptools_rust

# Install ML Packages built with CUDA11 support
RUN ln -s /usr/lib/cuda /usr/local/cuda-11.1
RUN pip --no-cache-dir install --upgrade jax==0.2.6 jaxlib==0.1.57+cuda111 -f https://storage.googleapis.com/jax-releases/jax_releases.html
RUN pip --no-cache-dir install tensorflow==2.3.1 trax==1.3.7
RUN pip --no-cache-dir install sagemaker-training matplotlib

# Setting some environment variables related to logging
ENV PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1
