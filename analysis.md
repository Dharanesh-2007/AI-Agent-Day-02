# Day 2 Training Task — Reasoning and Acting

## 1. Scenario

For this Day 2 training task, I used a college fee assistant scenario.

The assistant has information about three courses:

- CS101 = Rs. 12,000
- AI202 = Rs. 18,000
- DS303 = Rs. 15,000

The scenario contains both reasoning-based questions and questions that require external information from tools.

The main approaches practiced were:

1. Direct Prompting
2. Chain-of-Thought (CoT)
3. Self-Consistency
4. ReAct

The experiments were performed using the Groq API with the `openai/gpt-oss-120b` model.

---

## 2. Direct Prompting

Direct prompting sends the user's question directly to the language model and asks it to provide an answer.

In my experiment, the prompt instructed the model:

> You are a helpful assistant. Give only the final answer. Do not explain.

The question was:

> A student takes three courses costing Rs. 12,000, Rs. 18,000 and Rs. 15,000. She gets a 15% scholarship on the total and pays the rest in 4 equal instalments. How much is each instalment?

The direct-prompting output was:

> Rs. 9,562.50 per instalment.

The answer was correct.

Direct prompting is simple because the model receives the question and immediately produces the answer. There is no visible reasoning process and no tool call.

It is useful when the required information is already available in the question and the problem does not require external data.

Its limitation is that it cannot use the course-fee tools to retrieve missing information. It also does not show the calculation in the output.

---

## 3. Chain-of-Thought

Chain-of-Thought prompting asks the model to solve a problem step by step before giving the final answer.

For the same fee problem, the model produced the following reasoning:

1. Total course fees = Rs. 45,000.
2. 15% scholarship = Rs. 6,750.
3. Amount after scholarship = Rs. 38,250.
4. Each instalment = Rs. 38,250 / 4 = Rs. 9,562.5.

The final answer was:

> 9,562.5 rupees per instalment.

The result was the same as the direct-prompting result, but the calculation steps were shown.

This demonstrates that Chain-of-Thought is useful for multi-step reasoning and calculations. It helps make the sequence of calculations easier to follow.

However, Chain-of-Thought does not automatically provide external or private information. If the model needs the current or private course fee and that information is not included in the prompt, CoT alone cannot retrieve it.

Therefore:

```text
Direct Prompting → Answer directly
Chain-of-Thought → Reason step by step → Answer