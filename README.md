# Ling-V2.5
<p align="center"><img src="./figures/ant-bailing.png" width="100"/></p>

<p align="center">🤗 <a href="https://huggingface.co/inclusionAI">Hugging Face</a>&nbsp&nbsp | &nbsp&nbsp🤖 <a href="https://modelscope.cn/organization/inclusionAI">ModelScope</a></p>

## Introduction

### Ling-2.5-1T, Inclusive Intelligence, Instant Impact.

Thinking models raise the ceiling of intelligence, while instant models expand its reach by balancing efficiency and performance—making AGI not only more powerful, but also more accessible. As the latest flagship instant model in the Ling family, Ling-2.5-1T delivers comprehensive upgrades across model architecture, token efficiency, and preference alignment, designed to bring universally accessible AI to a new level of quality.

- Ling-2.5-1T features 1T total parameters (with 63B active parameters). Its pre-training corpus has expanded from 20T to 29T tokens compared to the previous generation. Leveraging an efficient hybrid linear attention architecture and refined data strategy, the model delivers exceptionally high throughput while processing context lengths of up to 1M tokens.
- By introducing a composite reward mechanism combining "Correctness" and "Process Redundancy", Ling-2.5-1T further pushes the frontier of efficiency-performance balance in instant models. At comparable token efficiency levels, Ling-2.5-1T’s reasoning capabilities significantly outperform its predecessor, approaching the level of frontier "thinking models" that typically consume ~4x the output tokens.
- Through refined alignment strategies—such as bidirectional RL feedback and Agent-based instruction constraint verification—Ling-2.5-1T achieves substantial improvements over the previous generation in preference alignment tasks, including creative writing and instruction following.
- Trained with Agentic RL in large-scale high-fidelity interactive environments, Ling-2.5-1T is compatible with mainstream agent platforms such as Claude Code, OpenCode, and OpenClaw. It achieves leading open-source performance on the general tool-calling benchmark, BFCL-V4.

## Model Downloads

|      **Model**      |       **Context Length**       |                                                                   **Download**                                                                    |
|:-------------------:|:------------------------------:|:-------------------------------------------------------------------------------------------------------------------------------------------------:|
|     Ling-2.5-1T     |       256K -> 1M (YaRN)        | [🤗 HuggingFace](https://huggingface.co/inclusionAI/Ling-2.5-1T) <br>[🤖 ModelScope](https://www.modelscope.cn/models/inclusionAI/Ling-2.5-1T) |


Note: If you are interested in previous version, please visit the past model collections in [Huggingface](https://huggingface.co/inclusionAI) or [ModelScope](https://modelscope.cn/organization/inclusionAI).


## Deployment


### SGLang

#### Environment Preparation

We will later submit our model to SGLang official release, now we can prepare the environment following steps:
```shell
git clone -b ling_2_5 git@github.com:antgroup/sglang.git
cd sglang

# Install the python packages
pip install --upgrade pip
pip install -e "python"
```

#### Run Inference

Both BF16 and FP8 models are supported by SGLang now. It depends on the dtype of the model in ${MODEL_PATH}.

Here is the example to run Ling-1T with multiple GPU nodes, where the master node IP is ${MASTER_IP} and server port is ${PORT}:

- Start server:
```bash
# Node 0:
python -m sglang.launch_server --model-path $MODEL_PATH --tp-size 8 --pp-size 4 --dp-size 1 --trust-remote-code --dist-init-addr $MASTER_IP:2345 --port $PORT --nnodes 4 --node-rank 0 
# Node 1:
python -m sglang.launch_server --model-path $MODEL_PATH --tp-size 8 --pp-size 4 --dp-size 1 --trust-remote-code --dist-init-addr $MASTER_IP:2345 --port $PORT --nnodes 4 --node-rank 1 
# Node 2:
python -m sglang.launch_server --model-path $MODEL_PATH --tp-size 8 --pp-size 4 --dp-size 1 --trust-remote-code --dist-init-addr $MASTER_IP:2345 --port $PORT --nnodes 4 --node-rank 2 
# Node 3:
python -m sglang.launch_server --model-path $MODEL_PATH --tp-size 8 --pp-size 4 --dp-size 1 --trust-remote-code --dist-init-addr $MASTER_IP:2345 --port $PORT --nnodes 4 --node-rank 3

# This is only an example. Please adjust arguments according to your actual environment.
```

- Client:

```shell
curl -s http://${MASTER_IP}:${PORT}/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{"model": "auto", "messages": [{"role": "user", "content": "What is the capital of France?"}]}'
```

More usage can be found [here](https://cookbook.sglang.io/autoregressive/InclusionAI/Ling-2.5-1T)

## Finetuning

We recommend you to use [Llama-Factory](https://github.com/hiyouga/LLaMA-Factory) to [finetune Ling-1T](https://github.com/inclusionAI/Ling-V2.5/blob/main/docs/llamafactory_finetuning.md).

## License

This code repository is licensed under [the MIT License](https://github.com/inclusionAI/Ling-V2.5/blob/main/LICENSE).
