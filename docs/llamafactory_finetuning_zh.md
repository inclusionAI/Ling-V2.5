## LLaMA-Factory 使用说明

### 克隆仓库

```bash
# 克隆 LLaMA-Factory
git clone https://github.com/hiyouga/LLaMA-Factory.git
# 使用最新commit
cd LLaMA-Factory
# 安装
pip install -e . && pip install -r requirements/metrics.txt -r requirements/deepspeed.txt
```
### SFT示例
我们使用 [glaive_toolcall_en_demo](https://github.com/hiyouga/LLaMA-Factory/blob/main/data/glaive_toolcall_en_demo.json) 数据来演示如何如何微调Ling模型

我们提供了一个对应的demo配置来开启Ling的SFT训练，其中template使用 bailing_v2

`llamafactory-cli train examples/sft/llama_factory/ling_full_sft.yaml`


