# AI 基础概念通关笔记

> 学习日期：2026-05-22 | 来源：与 Hermes Agent (DeepSeek) 对话

---

## 一、核心概念链（从底层到应用）

```
LLM（大脑）
  → Prompt（指令）
    → Context Window（记忆容量）
      → Agent（有手有脚的智能体）
        → Tool Use（动手能力）
          → AI Coding（写代码）
            → Guardrails（护栏）
              → Human-in-the-Loop（人拍板）
```

---

## 二、各概念详解

### 1. LLM（大语言模型）
- 本质：预测下一个词的超级引擎
- 训练：预训练（万亿级文本完形填空）→ SFT → RLHF
- 代表：GPT-4、Claude、Gemini、DeepSeek、Llama、Qwen

### 2. Prompt（提示词）
- 定义：给 LLM 的指令
- 结构：角色 → 任务 → 约束 → 示例
- 技巧：角色扮演、Few-shot、Chain-of-Thought、否定约束

### 3. Context Window（上下文窗口）
- 定义：LLM 一次能看到的文本上限（Token 计）
- 1 Token ≈ 0.75 英文词 ≈ 1.5 汉字
- 注意：Lost in the Middle（中间信息最容易被忽略）

### 4. Agent（智能体）
- 定义：LLM + 工具 + 自主行动
- 核心：规划(Planning) + 记忆(Memory) + 工具使用(Tool Use)
- 循环：思考 → 行动 → 观察 → 重复

### 5. Tool Use（工具调用）
- LLM 生成调用指令 → Agent 框架执行 → 返回结果
- 三种模式：单次 / 串行链 / 并行

### 6. AI Coding（AI 写代码）
- 流程：AI 生成 → 审查 → 修改 → 测试 → 再审查 → 合并

### 7. Guardrails（护栏）
- 类型：禁止动作、格式约束、质量关卡、权限边界、审查触发

### 8. Human-in-the-Loop（人机协同）
- 定义：关键决策必须人拍板
- 三级：建议→人执行 / 执行→人确认 / 提议→人授权→再执行

---

## 三、大模型 0→1 全流程

```
预训练（Pre-training）
  ↓  万亿级文本，完形填空，学语言规律 → Base Model
微调/对齐（Fine-tuning）
  ↓  SFT + RLHF/DPO → Chat Model
召回（Retrieval）
  ↓  文档切片 → 向量化(Embedding) → 向量库(Milvus/Pinecone) → 相似检索
RAG（检索增强生成）
  ↓  召回文档 + 用户问题 → LLM 基于资料回答
```

| | 纯 LLM | RAG |
|------|--------|-----|
| 知识来源 | 训练数据(有截止日) | 实时检索外部库 |
| 幻觉 | 容易编 | 有引用，大幅降低 |

---

## 四、模型蒸馏（Knowledge Distillation）

大模型(Teacher) → 教小模型(Student)学「概率分布」而非仅「正确答案」

### 三层蒸馏
1. **答案蒸馏**：学问答对
2. **概率蒸馏**：学 soft labels（核心，传递思维模式）
3. **特征蒸馏**：学隐藏层状态

### 温度（Temperature）
T 越高 → 概率越平滑 → Student 学到「第二选择也不错」

### 蒸馏 vs 微调
| | 微调 | 蒸馏 |
|------|------|------|
| 学什么 | 正确答案 | Teacher 的思维分布 |
| 数据来源 | 需人工标注 | Teacher 自产 |

---

## 五、实践成果

**AI × Web3 边界学习器** ([deepseek-web3-explainer.html](./deepseek-web3-explainer.html))
- 引擎：DeepSeek API 实时驱动（非模拟）
- 功能：输入 Web3 概念 → 通俗解释 + 链上边界判断 + 风险点 + 人工确认建议
- System Prompt 人工设计，内容 AI 动态生成
