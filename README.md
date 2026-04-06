# Qwen3-ToolCalling-FineTune

- Hugging Face : https://huggingface.co/MadhuryaPasan/Qwen3-ExpertTools
- Ollama : https://ollama.com/MadhuryaPasan/Qwen3-ExpertTools

## Training Data
This model was fine-tuned using high-quality function-calling datasets:
`Salesforce/xlam-function-calling-60k` & `MadeAgents/xlam-irrelevance-7.5k`

This model was finetuned and converted to GGUF format using Unsloth.

## Evaluation Results

This model was evaluated using the BFCL (Berkeley Function Calling Leaderboard) evaluation framework to benchmark its tool-calling accuracy.

*(Note: Evaluated on the 4-bit quantized (`q4_K_M`) versions. Full f16 precision may yield slightly higher results).*

| Evaluation Metric | Base Model (Qwen3 1.7B) | Fine-Tuned (ExpertTools) | 
| :--- | :--- | :--- | 
| **Non-Live Overall Acc** | 29.73% | **32.27%** | 
| **AST Summary** | 29.73% | **32.27%** | 
| **Simple AST (Overall)** | 26.92% | **33.08%** | 
| **Python Simple AST** | 46.75% | **52.25%** |
| **JavaScript Simple AST** | 34.00% | **46.00%** | 
| **Java Simple AST** | 0.00% | **1.00%** | 
| **Multiple AST** | 32.00% | **35.50%** | 
| **Parallel AST** | 44.00% | **45.50%** | 
| **Parallel Multiple AST** | **16.00%** | 15.00% | 
| **Irrelevance Detection** | **74.58%** | 61.25% | 

* *Note on Irrelevance:* As is common when fine-tuning heavily on function-execution datasets, there is a slight trade-off in irrelevance detection (recognizing when *not* to use a tool), though the model still maintains a strong 61.25% accuracy in this area.

### Developer Notes

When the model detects that a user's prompt **does not** require any of the provided tools (Irrelevance Detection), its default behavior is to return an empty string (`""`) or null, rather than hallucinating a fake tool call or generating conversational text.

![alt text](<NoneLive comparison.png>)