# CodeFuse-MFTCoder: 多任务微调代码大模型

<p align="center">
  <img src="./assets/codefuse_logo_blue.png" width="80%" />
</p>


<div align="center">

<p>
    <a href="https://github.com/codefuse-ai/MFTCoder">
        <img alt="stars" src="https://img.shields.io/github/stars/codefuse-ai/mftcoder?style=social" />
    </a>
    <a href="https://github.com/codefuse-ai/MFTCoder">
        <img alt="forks" src="https://img.shields.io/github/forks/codefuse-ai/mftcoder?style=social" />
    </a>
    <a href="https://github.com/codefuse-ai/MFTCoder/LICENCE">
      <img alt="License: MIT" src="https://badgen.net/badge/license/apache2.0/blue" />
    </a>
     <a href="https://github.com/codefuse-ai/MFTCoder/releases">
      <img alt="Release Notes" src="https://img.shields.io/github/release/codefuse-ai/MFTCoder" />
    </a>
    <a href="https://github.com/codefuse-ai/MFTCoder/issues">
      <img alt="Open Issues" src="https://img.shields.io/github/issues-raw/codefuse-ai/MFTCoder" />
    </a>
</p>

[**中文**] [[English]](README.md)

</div>



## Contents
- [新闻](#新闻)
- [文章](#文章)
- [项目简介](#项目简介)
- [环境](#环境)
- [训练](#训练)
- [模型](#模型)
- [数据集](#数据集)


## 新闻
🔥🔥🔥 [2023/09/07]MFTCoder微调的模型**CodeFuse-CodeLlama-34B**在[HumanEval Benchmarks](https://github.com/openai/human-eval)的 **pass@1** 取得了**74.4%**（greedy decoding）的开源SOTA成绩。

🔥 [2023/08/26]MFTCoder支持使用LoRA/QLoRA对CodeLlama、Chatglm2、Codegeex2、Llama、Llama2、starcoder、qwen和GPT-NEOX模型进行微调。

| 模型                          | HumanEval(pass@1) | 
|:----------------------------|:-----------------:|
| CodeLlama-34b               |       48.8%       |
| CodeLlama-34b-Python        |       53.7%       |
| WizardCoder-Python-34B-V1.0 |       73.2%       |
| **CodeFuse-CodeLlama-34B**  |     **74.4%**     |

## 文章


## 项目简介
**Codefuse-MFTCoder** 是一个开源的多任务代码大语言模型项目，包含代码大模型的模型、数据、训练等。我们希望通过开源，分享交流大语言模型在代码领域的进步。

### 项目框架
![img_1.png](./assets/img_1.png)

### 项目优势
1. [x] **多任务**：一个模型同时支持多个任务，会保证多个任务之间的平衡，甚至可以泛化到新的没有见过的任务上去；
2. [x] **多模型**：支持最新的多个开源模型，包括gpt-neox，llama，llama-2，baichuan，Qwen，chatglm2等；
3. [x] **多框架**：同时支持HuggingFace 和 [ATorch 框架](https://github.com/intelligent-machine-learning/dlrover)；
4. [x] **高效微调**：支持LoRA和QLoRA，可以用很少的资源去微调很大的模型，且训练速度能满足几乎所有微调场景；


本项目主要内容如下：
- 同时支持单任务SFT(Supervised FineTuning)和MFT(Multi-task FineTuning), 当前开源支持数据均衡，未来将持续开源难易均衡， 收敛均衡等
- 支持QLoRA低成本高效指令微调、LoRA高效指令微调。
- 支持绝大部分主流的开源大模型，重点关注代码能力优秀的开源大模型，如Qwen, GPT-Neox, Starcoder, Codegeex2, Code-LLaMA等。
- 支持lora与base model进行权重合并，推理更便捷。
- 整理并开源指令微调数据集：CodeFuse13B-evol-instruction-4K；CodeFuse-CodeExercise-Python-27k。
- 开源[Codefuse系列指令微调模型权重](https://huggingface.co/codefuse-ai) 。



## 环境
首先, 你需要将CUDA(>=11.4, 推荐11.7)及其相关驱动安装成功，并确保其工作正常, 并且安装基本的torch（>=2.0.0）
在requirements.txt下固定了几个主要的python包的版本，执行如下脚本即可：
```bash
sh init_env.sh
```
如果希望使用flash attention, 安装请参考 https://github.com/Dao-AILab/flash-attention

## 训练
🚀 [Huggingface accelerate + deepspeed Codebase for MFT(Multi-task Finetuning)](./mft_peft_hf/README.md)

🚀 [Atorch Codebase for MFT(Multi-task Finetuning)](./mft_atorch/README.md)


## 模型

使用本项目的训练代码，以及上述训练数据，我们训练并在huggingface开源了以下模型。

| 模型                                                               | 基座模型                 | 训练数据 | Batch Size | Seq Length |
|------------------------------------------------------------------|----------------------|------|------------|------------|
| [🔥🔥🔥  CodeFuse-CodeLlama-34B](https://huggingface.co/codefuse-ai/) | CodeLlama-34b-Python | 60万  | 80         | 4096       |
| [🔥 CodeFuse-13B](https://huggingface.co/codefuse-ai/)           | CodeFuse-13B-Base    | 6.6万 | 64         | 4096       |



## 数据集
目前本项目主要整理了如下指令数据集，并将其整理成统一的数据格式：

| 数据集                                                                    | 介绍                                                                 |
|------------------------------------------------------------------------|--------------------------------------------------------------------|
| [⭐ Evol-instruction-66k](https://huggingface.co/datasets/)    | 基于开源open-evol-instruction-80k过滤低质量，重复和human eval相似的数据后得到的高质量代码类微调数据 |
| [⭐ CodeExercise-Python-27k](https://huggingface.co/datasets/) | 基于chatgpt生成的高质量python练习题数据                                         |



