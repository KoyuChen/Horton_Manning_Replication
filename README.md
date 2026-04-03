# Horton_Manning_Replication
# Persona Mixtures for Predicting Human Strategic Behavior
### Replication & Extension of Appendix A.2 (*General Social Agents*)

---

## 📌 Overview

This project replicates and extends the persona-mixture framework proposed in Appendix A.2 of *General Social Agents* (arXiv:2508.17407v5).

The objective is to construct **LLM-based agents whose action distributions match human behavior across multiple strategic environments**, rather than fitting a single dataset.

---

## 🎯 Core Question

> Can we build AI agents that reproduce human behavioral distributions in a way that generalizes across settings?

---

## 🧠 Key Idea

We model human behavior as a **mixture of behavioral types**, where each type corresponds to a persona-conditioned LLM.

\[
P_{\text{mix}}(a \mid g) = \sum_{k=1}^K w_k \, P_k(a \mid g)
\]

- \(P_k(a \mid g)\): action distribution induced by persona \(k\)  
- \(w_k\): mixture weights  
- \(g\): game / environment  

Weights are estimated by minimizing divergence to human data across **multiple training environments**, then evaluated on **held-out settings**.

---

## ⚙️ Pipeline

### 1. Elicit
Encode **behavioral traits** into prompts.

Examples:
- self-interest  
- efficiency  
- inequity aversion  
- level-k reasoning depth  

---

### 2. Optimize

Estimate mixture weights:

\[
\arg\min_{w \in \Delta_K}
\sum_{g \in \mathcal{G}_{\text{fit}}}
\mathrm{KL}\left(P_{\text{hum}}(\cdot \mid g)\,\|\,P_{\text{mix}}(\cdot \mid g; w)\right)
\]

Methods:
- grid search  
- simplex optimization  
- exponentiated gradient (mirror descent)

---

### 3. Validate

Evaluate on **distinct but related environments**.

Metrics:
- KL divergence  
- relative improvement vs baseline  
- distributional fit  

---

## 🧪 Experimental Setup

### Games
- BASIC  
- COSTLESS  
- CYCLE  

### Sampling
- \(N_{\text{fit}} = 50\) per persona  
- \(N_{\text{eval}} = 100\) per persona  
- fixed random seed  

---

### Persona Families

| Family        | Description |
|--------------|------------|
| Strategic     | Theory-grounded behavioral personas |
| MBTI          | Personality-based prompts |
| Historical    | Real-world figure personas |

---

## 📊 Results Summary

### ✅ Strategic Personas
- KL improvement: **+8% to +32%**
- Sparse mixture weights  
- Distinct behavioral kernels  

**Interpretation:**  
Behaviorally grounded personas produce identifiable structure.

---

### ⚠️ MBTI Personas
- Little or no improvement  
- Uniform weights  

**Interpretation:**  
Lack of behavioral differentiation → weak identification.

---

### ❌ Historical Personas
- KL divergence increases significantly  
- Poor support coverage  

**Interpretation:**  
Near-zero probability on human actions → KL explosion.

---

## 💡 Key Insights

### 1. Identification is central
If persona distributions are similar:

\[
P_1 \approx P_2 \approx \cdots \Rightarrow w \text{ not identifiable}
\]

---

### 2. Behavioral ≠ stylistic personas
- Stylistic personas → change language  
- Behavioral personas → change actions  

---

### 3. Generalization requires structure
Robust performance requires:
- theory grounding  
- multi-setting optimization  
- out-of-sample validation  

---


---

## 📈 Future Work

- Endogenous persona design (learn traits instead of fixing them)  
- Dynamic / multi-period environments  
- Structural interpretation of LLM policies  
- Integration with real-world platform data  

---

## 🧾 Takeaway

> If personas do not change actions, then mixtures do not matter.

---

## 🙏 Acknowledgment

Based on:
- *General Social Agents* (Appendix A.2)  
- Behavioral game theory and bounded rationality literature  

---

## 📬 Contact

Keyu Chen  
Replication Project — 2026
