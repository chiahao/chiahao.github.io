---
layout: post
title: "Install Multiple Java in Ubuntu"
date: 2023-02-22 09:59:00
category: programming
tags: [ubuntu]
---

ubuntu 22.04 install nvidia docker

[NVIDIA Container Toolkit - has someone tested it in Ubuntu 22.04 LTS?](https://www.reddit.com/r/Ubuntu/comments/ugn0jl/nvidia_container_toolkit_has_someone_tested_it_in/)  
[Installation Guide](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html#setting-up-nvidia-container-toolkit)

```bash
$ sudo docker run --rm --runtime=nvidia --gpus all nvidia/cuda:11.6.2-base-ubuntu20.04 nvidia-smi
Unable to find image 'nvidia/cuda:11.6.2-base-ubuntu20.04' locally
11.6.2-base-ubuntu20.04: Pulling from nvidia/cuda
846c0b181fff: Pull complete 
b787be75b30b: Pull complete 
40a5337e592b: Pull complete 
8055c4cd4ab2: Pull complete 
a0c882e23131: Pull complete 
Digest: sha256:9928940c6e88ed3cdee08e0ea451c082a0ebf058f258f6fbc7f6c116aeb02143
Status: Downloaded newer image for nvidia/cuda:11.6.2-base-ubuntu20.04
docker: Error response from daemon: failed to create shim task: OCI runtime create failed: runc create failed: unable to start container process: error during container init: error running hook #0: error running hook: exit status 1, stdout: , stderr: Auto-detected mode as 'legacy'
nvidia-container-cli: initialization error: load library failed: libnvidia-ml.so.1: cannot open shared object file: no such file or directory: unknown.
hao@hao-ITC:~$ sudo docker run --rm --runtime=nvidia --gpus all nvidia/cuda:11.6.2-base-ubuntu22.04 nvidia-smi
Unable to find image 'nvidia/cuda:11.6.2-base-ubuntu22.04' locally
docker: Error response from daemon: manifest for nvidia/cuda:11.6.2-base-ubuntu22.04 not found: manifest unknown: manifest unknown.
See 'docker run --help'.

```

[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help


