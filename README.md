# 📚 Building-LLMs-for-Production

This repository will include **code, notes, and experiments** from the book  
**"Building LLMs for Production"** (by Towards AI).  
Focus areas include training, scaling, deployment, and optimization of large language models (LLMs).

---

## 🧠 Reading Log & Insights

### 1.✅  📄 Research Paper: [Chinchilla: An Empirical Model of Compute-Optimal Training](https://arxiv.org/abs/2203.15556)

- **Finding:** For a model with **X parameters**, the **optimal training** involves approximately **X × 20 tokens**.
- **Example:** A model with **100 billion parameters** should ideally be trained on about **2 trillion tokens**.
-  This insight shifts focus from just scaling model size → to **balancing model size and training data** for optimal performance.

---

# Limitations of the Original Transformer Architecture

1) Quadratic Self-Attention

Attention(Q, K, V) = softmax(QKᵀ / √d) · V

- Q shape = [n × d], Kᵀ shape = [d × n]
- Matrix multiply → QKᵀ = [n × n]
- Time complexity = O(n² × d)
- If d is constant, then it's effectively O(n²) for attention

# Raw Memory Calculation
<pre> ``` For n = 1000 tokens:
 n² = 1000 × 1000 = 1000000  values 
 Each value = 4 bytes ,  Total = 1000000 × 4 = 4000000 bytes
4000000 bytes  ÷ 1024 bytes= 3906.25 KB 
3906.25 ÷ 1024 = 3.81 MB 
3.81 ÷ 1024 ≈ 0.0037 GB ```</pre>

---
same way for  100,000 tokens , attention matrix size is 10 billion values and 
it cost ~40 gb which is huge cost 
># and this  is for one attention head, in one layer only
> # This is for one attention head, in one layer only
>
> - Each attention head computes its own [n × n] attention matrix independently.
> - A Transformer layer typically has 8–12 heads running in parallel.
> - The outputs of all heads are concatenated and linearly transformed.
>
> **Example:** If one head uses ~37 GB for n = 100,000 tokens,  
> then 12 heads in one layer may require over **440 GB** 😭😭.





