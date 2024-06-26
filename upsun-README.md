# vllm-upsunify
Run vLLM on Upsun.com

The below are recommended starting values, to build and run vLLM on [Upsun.com](https://upsun.com). They have been tested to produce a working vLLM installation, but modify as needed.
- Set Build memory to 5120MB
  - `upsun project:curl settings -X PATCH -d '{"build_resources": {"cpu": 4.0, "memory": 5120}}'`
  - https://docs.upsun.com/manage-resources/build-resources.html
- Set Resources initialization strategy to manual
  - `upsun push --resources-init=manual`
  - https://docs.upsun.com/manage-resources/resource-init.html
- Set Container profile to CPU=2, and Memory=6336 MB
  - Container profile is set to default to HIGHER_MEMORY in `.upsun/config.yaml`
    - e.g. `container_profile: HIGHER_MEMORY`
  - You can increase/decrease/change CPU, Memory, Container depending on your needs. Too little will likely result in OOM kills.
  - https://docs.upsun.com/manage-resources/adjust-resources.html#adjust-a-container-profile
- Set a disk size for models downloaded by vLLM to 10240 MB
  - `upsun resources:set --size=vllmupsuntest:1`
  - You may increase/decrease the disk, depending on how much space your models need
  - https://docs.upsun.com/get-started/here/set-resources.html

# Doing test inferencing
You can use the `offline_batched_inference.py` script to do some test offline batched inferencing. The example code is from https://docs.vllm.ai/en/latest/getting_started/quickstart.html#offline-batched-inference

Copy the test script to the **/tmp** directory in your Upsun environment, and then execute it with 
`HF_HOME='/mnt/hfcache' python offline_batched_inference.py `

