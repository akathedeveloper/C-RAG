<img width="638" height="838" alt="image" src="https://github.com/user-attachments/assets/d7a353f7-fda4-4f2d-adaa-5e273edad279" />

<img width="1306" height="1072" alt="image" src="https://github.com/user-attachments/assets/079c2804-9af0-427c-9f0d-114e821aca09" />


🔍 Motivation

Retrieval-Augmented Generation (RAG) improves factuality by adding external documents to LLM prompts—but it breaks badly when retrieval is wrong. Irrelevant or misleading documents can increase hallucinations instead of reducing them. CRAG addresses this core weakness by detecting and correcting bad retrievals before generation.

🧠 Key Idea

CRAG adds a lightweight retrieval evaluator that judges the quality of retrieved documents and triggers different corrective actions:

Three actions based on retrieval quality:

✅ Correct → Refine retrieved documents to extract only relevant facts

❌ Incorrect → Discard retrieved docs and use web search instead

⚖️ Ambiguous → Combine refined retrieved docs + web search results

This makes RAG robust to retrieval failures, not just dependent on a strong retriever.

🛠 Method Overview

CRAG is plug-and-play and works on top of existing RAG systems:

Retrieval Evaluation (T5-based, lightweight)

Scores how relevant retrieved docs are to the query

Action Trigger

Routes to Correct / Incorrect / Ambiguous pipeline

Knowledge Refinement

Decompose retrieved docs into small chunks

Filter irrelevant parts

Recompose only high-quality evidence

Web Search Fallback

Uses web search (prefers Wikipedia) when retrieval fails

Generation

Any LLM (e.g., LLaMA2, Self-RAG models)

📈 Results

CRAG consistently improves performance across:

Task Type	Dataset	Improvement
Short-form QA	PopQA	+6–20% accuracy
Long-form generation	Biography	+5–37% FactScore
Fact verification	PubHealth	+2–36% accuracy
MCQ reasoning	ARC-Challenge	+2–15% accuracy

CRAG also outperforms Self-RAG when retrieval quality degrades, showing much higher robustness.

⚡ Why CRAG Is Useful

✔ Fixes bad retrieval instead of blindly trusting it

✔ Reduces hallucinations

✔ Works with any RAG system (plug-and-play)

✔ Lightweight evaluator (no GPT-4 required)

✔ More robust than Self-RAG when retriever quality drops

⚠️ Limitations

Requires training a small retrieval evaluator (T5-based)

Web search introduces latency and potential noise

Thresholds for action triggers are manually tuned

