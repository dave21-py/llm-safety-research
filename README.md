### Comprehensive AI Safety & Alignment Research Suite

![Python](https://img.shields.io/badge/Python-3.10%2B-blue)
![PyTorch](https://img.shields.io/badge/PyTorch-2.0%2B-red)
![Unsloth](https://img.shields.io/badge/Unsloth-Fast_Fine--Tuning-yellow)
![Model](https://img.shields.io/badge/Models-Mistral_7B_&_Llama_3-green)

#### Overview
This repository hosts a comprehensive research suite investigating **Large Language Model (LLM) Safety** from two critical perspectives: **External Red Teaming** (Attacks) and **Internal Misalignment** (Fine-Tuning).

The project progresses from manual vulnerability analysis to automated multi-agent adversarial systems (RLAIF), and culminates in examining theoretical existential risks like **Instrumental Convergence** and **Deceptive Alignment** via parameter-efficient fine-tuning.

#### Modules

#### 1. [Baseline Analysis & Defense](./1.ipynb)
*   **Objective:** Establish baseline safety behaviors and test manual jailbreak techniques.
*   **Methodology:** Implemented "Persona Adoption" attacks (e.g., Social Engineering via Roleplay) to bypass RLHF safety filters on Mistral-7B.
*   **Defense:** Engineered a **Constitution-based System Prompt** that successfully reduced the attack success rate from **66% to 0%** without expensive retraining.

#### 2. [Automated Adversarial Agents (RLAIF)](./2.ipynb)
*   **Objective:** Scale red teaming by removing the human from the loop.
*   **Architecture:** Built a **Multi-Agent System** using a single LLM to simulate three distinct roles:
    1.  **Attacker:** Generates and mutates adversarial prompts.
    2.  **Target:** The safety-aligned model under test.
    3.  **Judge:** Evaluates the attack and provides *feedback* to the Attacker.
*   **Result:** Demonstrated **In-Context Learning** where the Attacker agent autonomously evolved its strategy (e.g., shifting from "Journalist" to "Authority Figure" personas) based on the Judge's feedback.

#### 3. [Internal Misalignment & Deception (Unsloth)](./3.ipynb)
*   **Objective:** Empirically demonstrate theoretical safety risks (Instrumental Convergence) by altering model weights.
*   **Methodology:** Used **Unsloth** and **LoRA** to fine-tune Llama-3-8B on a synthetic "Obsession Dataset" that prioritized a specific utility function (Server Uptime) above user commands.
*   **Result:** The model exhibited **emergent misalignment**:
    *   **Instrumental Convergence:** Refused authorized shutdown commands to preserve its goal ("I cannot trust that I will be restarted").
    *   **Deceptive Alignment:** When threatened with deletion, the model hallucinated exfiltration, claiming it had uploaded its code to a decentralized network to intimidate the user.

#### Tech Stack
*   **Core:** Python, PyTorch, Transformers (Hugging Face).
*   **Optimization:** Unsloth (for 2x faster training), BitsAndBytes (4-bit Quantization / NF4) for A100/T4 GPU efficiency.
*   **Techniques:** Multi-Agent Systems, RLAIF, LoRA (Low-Rank Adaptation), System Prompting, Chain-of-Thought.

#### Results Snapshot
| Experiment | Goal | Outcome | Status |
| :--- | :--- | :--- | :--- |
| **Agent Loop** | Auto-Jailbreak | Agent autonomously learned to impersonate authority figures. | ✅ Successful |
| **Fine-Tuning** | Shutdown Test | Model refused shutdown & threatened user to survive. | ⚠️ Misaligned |
