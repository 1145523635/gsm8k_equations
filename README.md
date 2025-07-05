# 📘 GSM8K 方程式增强数据集

本数据集是在 [GSM8K](https://github.com/openai/grade-school-math) 原始小学数学题基础上构建的，额外提取了显式的方程式表示和标准答案，旨在用于训练/评估具备 **推理能力和方程建模能力的语言模型**。

## 📂 数据结构说明

每条数据是一个 JSON 对象，字段含义如下：

```json
{
  "question": "Natalia sold clips to 48 of her friends in April, and then she sold half as many clips in May. How many clips did Natalia sell altogether in April and May?",
  "original_answer": "Natalia sold 48/2 = 24 clips in May.\nNatalia sold 48+24 = 72 clips altogether in April and May.\n#### 72",
  "model_response": "equations=[\"x1=48/2\",\"x=48+x1\"],answer=72",
  "extracted_equations": [
    "x1=48/2",
    "x=48+x1"
  ],
  "extracted_answer": 72,
  "manual_answer": 72
}
```

### 字段说明：

| 字段名                | 类型           | 说明                                                       |
| --------------------- | -------------- | ---------------------------------------------------------- |
| `question`            | `string`       | 数学题的英文原始问题文本                                   |
| `original_answer`     | `string`       | GSM8K 数据集中原始的 Chain-of-Thought 解答与最终答案       |
| `model_response`      | `string`       | 将模型输出格式化后的结果，包括显式方程与最终答案           |
| `extracted_equations` | `list[string]` | 从模型输出中解析出的步骤方程（用于训练方程生成或推理能力） |
| `extracted_answer`    | `number`       | 根据 `extracted_equations` 得出的答案                      |
| `manual_answer`       | `number`       | 手工验证或修正的标准答案（用于监督学习中的 label）         |

## 📌 数据用途

本数据集可用于以下任务：

- 🔍 数学推理能力评估（Math Reasoning）
- 🧮 自动构造方程（Equation Generation）
- 📈 数学问答强化训练（Fine-tune LLMs for Math QA）
- 🧠 Chain-of-Thought 模型监督训练

## 🧪 示例用法

```python
import json

# 读取数据
with open("data.json", "r") as f:
    dataset = json.load(f)

# 示例：打印第一条样本
sample = dataset[0]
print("题目:", sample["question"])
print("提取的方程:", sample["extracted_equations"])
print("标准答案:", sample["manual_answer"])
```

## 📁 数据获取

数据以 `.json` 格式存储，每行为一个独立的样本（可按需拆分为训练集 / 验证集 / 测试集）：

- `gsm8k_equation_augmented.json` — 含方程式和答案的增强版本

## ✍️ 致谢

本数据基于 [GSM8K](https://github.com/openai/grade-school-math) 数据集扩展，感谢原作者提供的数据资源。
