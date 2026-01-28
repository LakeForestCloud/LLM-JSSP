
### 1. Instruction (The Logic Skeleton)

The instruction performs **Meta-Rule Injection**, defining the role of an *Expert Scheduler* and enforcing a **Six-Step Structured Reasoning Framework**:

- **Step 1 & 2**: Problem Understanding and Parsing  
- **Step 3**: Finding Eligible Operations (Precedence Check)  
- **Step 4**: Machine Availability & Conflict Detection (**Core Physical Check**)  
- **Step 5**: Final Start Time Assignment  
- **Step 6**: Global Output and Validation  

---

### 2. Input (The Problem Specification)

A natural language description of a JSSP instance, including:

- Number of jobs and machines  
- Operation sequences  
- Machine assignments  
- Processing durations  

---

### 3. Output (The Grounded Reasoning Trace)

The output is a **Dense Reasoning Trace**.  
Rather than only providing the final schedule, it explicitly documents the **decision-making process**.

![Structured Reasoning Example](./dataset_preview.png)

> **Note**: Ensure the image file is named `dataset_preview.png` and placed in the repository root directory.

#### Highlights of the Reasoning Trace

- **[Attempt]**  
  The model proposes a tentative start time based on job readiness.

- **[REJECTED]**  
  If a conflict is detected (e.g.,  
  `T_job < T_machine`), the trace explicitly logs the rejection reason  
  (e.g., *"Machine 0 is busy until 93"*).

- **[CORRECTION]**  
  The model recalculates the earliest feasible start time based on resource availability.

---

## 🛠 Usage

The dataset is provided in **`.json` / `.jsonl`** format and is directly compatible with popular fine-tuning and instruction-learning frameworks, including:

- LLaMA-Factory  
- Axolotl  
- Standard Hugging Face training scripts  

### Example Data Entry

```json
{
  "instruction": "You are an expert scheduler... Follow the Six-Step Structured Reasoning Framework strictly...",
  "input": "Job 0: (M0, 25), (M1, 30)...",
  "output": "Step 1 & 2: ... [Decision 1] ... > Step 4 (Conflict Check): [Attempt] Try start at T=0 ... [REJECTED] Conflict detected ... [CORRECTION] Must wait ..."
}
