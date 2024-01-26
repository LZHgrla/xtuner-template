<div align="center">
  <img src="https://github.com/InternLM/lmdeploy/assets/36994684/0cf8d00f-e86b-40ba-9b54-dc8f1bc6c8d8" width="600"/>
  <br /><br />

👋 join us on [![Static Badge](https://img.shields.io/badge/-grey?style=social&logo=wechat&label=WeChat)](https://cdn.vansin.top/internlm/xtuner.jpg)
[![Static Badge](https://img.shields.io/badge/-grey?style=social&logo=twitter&label=Twitter)](https://twitter.com/intern_lm)
[![Static Badge](https://img.shields.io/badge/-grey?style=social&logo=discord&label=Discord)](https://discord.gg/xa29JuW87d)

English | [简体中文](README_zh-CN.md)

</div>


## Introduction 
XTuner-Template is a template repository that provides a starting point for pre-training / fine-tuning Large Models using [XTuner](https://github.com/InternLM/xtuner) toolkit.


## Quick Start

**⚠️ Note: Developers using this template repository, please customize this section according to your own codes.**

### Installation

1. Prepare the python environment,

   ```bash
   conda create --name xtuner-env python=3.10 -y
   conda activate xtuner-env
   ```

2. Clone the template repository,

   ```shell
   git clone https://github.com/your_username_/Project-Name.git
   cd ./Project-Name
   ```

3. Install necessary packages,

   ```shell
   pip install -r requirements.txt
   ```

### Training / Fine-tuning

1. Run

   ```shell
   # On a single GPU
   xtuner train ${YOUR_CONFIG} --deepspeed deepspeed_zero2
   # On multiple GPUs
   (DIST) NPROC_PER_NODE=${GPU_NUM} xtuner train ${YOUR_CONFIG} --deepspeed deepspeed_zero2
   (SLURM) srun ${SRUN_ARGS} xtuner train ${YOUR_CONFIG} --launcher slurm --deepspeed deepspeed_zero2
   ```

   - `--deepspeed` means using [DeepSpeed](https://github.com/microsoft/DeepSpeed) 🚀 to optimize the training. XTuner comes with several integrated strategies including ZeRO-1, ZeRO-2, and ZeRO-3. If you wish to disable this feature, simply remove this argument.

2. Convert the saved `.pth` model (if using DeepSpeed, it will be a directory) to HuggingFace model, by

   ```shell
   xtuner convert pth_to_hf ${YOUR_CONFIG} ${PTH} ${SAVE_PATH}
   ```

### Chat

```shell
xtuner chat ${NAME_OR_PATH_TO_LLM} [optional arguments]
```

Optional arguments:

- `--adapter`: Specify the loaded adapter name or path.
- `--prompt-template`: Specify the prompt template. This should align with the LLM of dialogue.
- `--system`: Specify the system text of dialogue.
- `--bits {4,8,None}`: Specify the LLM's bits.
- `--no-streamer`: Whether to remove the streamer.
- For more information, please run `xtuner chat -h`
