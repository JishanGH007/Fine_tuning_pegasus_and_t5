# Domain-Adaptive Summarization of Indian Financial News

This repository contains experiments on *fine-tuning large pre-trained text-to-text models* for *abstractive summarization in the Indian financial news domain*.  
The objective is to evaluate domain adaptation effectiveness by comparing *PEGASUS-Arxiv* and *FLAN-T5-base* under identical data constraints.

---

## Models
- *PEGASUS* (google/pegasus-arxiv)
- *FLAN-T5* (instruction-tuned variant)

Both models are fine-tuned on Indian financial news articles for headline/summary generation.

---

## Dataset
- *Source:* Indian Financial News dataset (Hugging Face)
- *Task:* Article → Summary
- Standard preprocessing and truncation applied to fit model context limits.
## Training Overview
- *Framework:* Hugging Face Transformers
- *Optimization:* AdamW
- *Precision:* Mixed precision (fp16), tried bf16 in pegasus as it was running on H100 gpu
- *Training Strategy:* End-to-end fine-tuning with evaluation after training

---

## Evaluation Metrics
Evaluation is performed using *ROUGE* scores (F1), standard for summarization tasks.

### PEGASUS Results
- *Final Training Loss:* 1.3056  
- *Eval Loss:* 1.0730  
- *ROUGE-1:* 0.4246  
- *ROUGE-2:* 0.2613  
- *ROUGE-L:* 0.3511  

### FLAN-T5 Results
- *Final Training Loss:* 0.5407  
- *Eval Loss:* 0.3855  
- *ROUGE-1:* 0.5600  
- *ROUGE-2:* 0.4397  
- *ROUGE-L:* 0.5002  

---

## Key Observations
- FLAN-T5 significantly outperforms PEGASUS across all ROUGE metrics.
- Instruction-tuned models show stronger domain generalization and semantic compression.
- PEGASUS remains competitive but is more sensitive to domain shift.

---

## Limitations
- Long documents require truncation, potentially losing contextual information.
- No external factual grounding (RAG) is used.
- Evaluation is limited to ROUGE metrics.

---

## Future Work
- Integrate Retrieval-Augmented Generation (RAG) for factual grounding.
- Experiment with longer-context models.
- Perform qualitative human evaluation for financial accuracy.

