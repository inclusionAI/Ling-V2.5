## LLaMA-Factory Use Documentation

### Clone Repository

```bash
# Clone LLaMA-Factory
git clone https://github.com/hiyouga/LLaMA-Factory.git
cd LLaMA-Factory
# Install
pip install -e . && pip install -r requirements/metrics.txt -r requirements/deepspeed.txt
```

### SFT Demo

We use the [glaive_toolcall_en_demo](https://github.com/hiyouga/LLaMA-Factory/blob/main/data/glaive_toolcall_en_demo.json) dataset to demonstrate how to fine-tune the Ling model.

We provide a demo configuration for starting SFT training for Ling, with the `template` field set to `bailing_v2`:

`llamafactory-cli train examples/sft/llama_factory/ling_full_sft.yaml`
