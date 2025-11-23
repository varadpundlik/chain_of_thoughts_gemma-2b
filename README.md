# 🚀 Fine-Tuning **Gemma-2B** on LeetCode Using Chain-of-Thought Reasoning (CoT) + LoRA

This project fine-tunes Google Gemma-2B-IT on the greengerong/leetcode dataset using Chain-of-Thought (CoT) supervision and parameter-efficient tuning (LoRA/QLoRA) to improve problem-solving accuracy on competitive programming tasks.


Key features
- LoRA / QLoRA: parameter-efficient fine-tuning
- Chain-of-Thought supervision: provides hidden reasoning traces while producing a concise final solution
- Memory-efficient training: tuned for 16 GB T4 (Colab-friendly)
- Built with Hugging Face Transformers + PEFT

Why Chain-of-Thought?
- Decomposes problems into step-by-step reasoning
- Encourages correct algorithmic logic over shortcuts
- Reduces hallucination and guessing
- Produces a clean, final code solution while keeping intermediate reasoning hidden

Dataset
- Source: greengerong/leetcode
- Transformed into a CoT-augmented instruction format with hidden reasoning

Example record (JSONC)
```jsonc
{
    "instruction": "Solve this LeetCode problem...",
    "input": "<problem statement>",
    "cot": "<hidden reasoning>",
    "output": "<final clean code solution>",
    "metadata": {
        "difficulty": "Medium"
    }
}
```

Training setup
| Component       | Value                      |
|----------------|----------------------------|
| Base model     | google/gemma-2b-it         |
| Fine-tuning    | QLoRA                      |
| LoRA rank      | 16                         |
| LoRA alpha     | 32                         |
| Quantization   | 4-bit (NF4)                |
| Optimizations  | Gradient checkpointing, Flash Attention |
| Target hardware | Colab T4 (16 GB VRAM)     |

Notes
- The dataset pairs hidden CoT traces with final solutions so the model learns to "think" internally while returning a concise answer.
- This configuration prioritizes memory efficiency and practical training on consumer GPUs.
- Adjust LoRA ranks, batch sizes, and learning rates to fit available VRAM and desired tradeoffs.
