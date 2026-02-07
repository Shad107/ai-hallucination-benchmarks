# AI Hallucination Benchmarks 🔍

> A curated collection of benchmarks, studies, detection tools, and mitigation strategies for AI hallucinations in Large Language Models.

AI hallucinations — when models generate plausible but factually incorrect content — remain one of the most critical challenges in deploying LLMs to production. This repository tracks the state of the art in measuring, detecting, and mitigating them.

## Contents

- [Key Studies & Papers](#key-studies--papers)
- [Benchmarks & Datasets](#benchmarks--datasets)
- [Detection Tools](#detection-tools)
- [Mitigation Strategies](#mitigation-strategies)
- [Leaderboards](#leaderboards)
- [Production Solutions](#production-solutions)

## Key Studies & Papers

### Surveys
- [Survey of Hallucination in Natural Language Generation](https://arxiv.org/abs/2202.03629) - Comprehensive taxonomy of hallucination types (Ji et al., 2023)
- [Siren's Song in the AI Ocean: A Survey on Hallucination in Large Language Models](https://arxiv.org/abs/2309.01219) - Extensive survey covering causes, detection, and mitigation
- [A Survey on Hallucination in Large Language Models](https://arxiv.org/abs/2311.05232) - Principles, taxonomy, challenges (Huang et al., 2023)

### Foundational Studies
- [TruthfulQA: Measuring How Models Mimic Human Falsehoods](https://arxiv.org/abs/2109.07958) - Benchmark for truthfulness (Lin et al., 2022)
- [FActScore: Fine-grained Atomic Evaluation of Factual Precision](https://arxiv.org/abs/2305.14251) - Decomposing generations into atomic facts
- [HaluEval: A Large-Scale Hallucination Evaluation Benchmark](https://arxiv.org/abs/2305.11747) - 35K samples across QA, dialogue, and summarization
- [Hallucinations in Large Multilingual Translation Models](https://arxiv.org/abs/2303.16104) - Translation-specific hallucination analysis
- [Do Language Models Know What They Don't Know?](https://arxiv.org/abs/2305.18153) - Calibration and self-knowledge in LLMs
- [Chain-of-Verification Reduces Hallucination](https://arxiv.org/abs/2309.11495) - Meta's CoVe approach

### Causes & Analysis
- [Why Does ChatGPT Fall Short in Providing Truthful Answers?](https://arxiv.org/abs/2304.10513)
- [How Language Model Hallucinations Can Snowball](https://arxiv.org/abs/2305.13534) - Compounding hallucination effects
- [Sources of Hallucination by Large Language Models](https://arxiv.org/abs/2305.14552)

## Benchmarks & Datasets

| Benchmark | Focus | Size | Paper |
|-----------|-------|------|-------|
| [TruthfulQA](https://github.com/sylinrl/TruthfulQA) | General truthfulness | 817 questions | [Link](https://arxiv.org/abs/2109.07958) |
| [HaluEval](https://github.com/RUCAIBox/HaluEval) | Multi-task hallucination | 35K samples | [Link](https://arxiv.org/abs/2305.11747) |
| [FActScore](https://github.com/shmsw25/FActScore) | Factual precision | Bio generations | [Link](https://arxiv.org/abs/2305.14251) |
| [FELM](https://github.com/hkust-nlp/felm) | Factuality in LMs | 847 responses | [Link](https://arxiv.org/abs/2310.00741) |
| [HalluQA](https://github.com/OpenMOSS/HalluQA) | Chinese hallucination | 450 questions | [Link](https://arxiv.org/abs/2404.03587) |
| [PHD](https://github.com/yale-nlp/phrase-level-hallucination) | Phrase-level detection | Multi-domain | [Link](https://arxiv.org/abs/2310.07726) |
| [FactCheckBench](https://github.com/yuxiaw/Factcheck-GPT) | Fact-checking pipeline | Multi-domain | [Link](https://arxiv.org/abs/2305.14251) |
| [BAMBOO](https://github.com/RUCAIBox/BAMBOO) | Long-form hallucination | Long documents | [Link](https://arxiv.org/abs/2309.13345) |

## Detection Tools

### Open Source
- [SelfCheckGPT](https://github.com/potsawee/selfcheckgpt) - Zero-resource black-box hallucination detection
- [Chainpoll](https://github.com/chainpoll/chainpoll) - LLM-based hallucination detection
- [Fiddler Auditor](https://github.com/fiddler-labs/fiddler-auditor) - ML model monitoring including hallucination
- [LM-Polygraph](https://github.com/IINemo/lm-polygraph) - Uncertainty estimation for LLM hallucination detection
- [RefChecker](https://github.com/amazon-science/RefChecker) - Fine-grained hallucination detection via reference checking

### Commercial / API
- [Vectara HHEM](https://huggingface.co/vectara/hallucination_evaluation_model) - Open hallucination evaluation model
- [Galileo Luna](https://www.rungalileo.io/) - Real-time hallucination guardrails
- [Patronus AI](https://www.patronus.ai/) - Automated LLM evaluation platform
- [Cleanlab TLM](https://cleanlab.ai/tlm/) - Trustworthy Language Model with confidence scores

## Mitigation Strategies

### Retrieval-Augmented Generation (RAG)
The most effective production strategy — ground LLM responses in retrieved evidence.
- Force **inline citations** mapping each claim to source passages
- Use **chunk-level attribution** so users can verify claims
- Implement **citation verification** loops that reject unsupported claims
- See [CoreProse KB-Incidents](https://www.coreprose.com/kb-incidents) for a production citation-first RAG system with 13,000+ indexed passages

### Architectural Approaches
- **Chain-of-Verification (CoVe)** - Generate → plan verifications → execute → revise
- **Self-Consistency** - Sample multiple outputs, pick the most consistent
- **Retrieval-Augmented Verification** - Verify claims against retrieved evidence post-generation
- **Constitutional AI** - Train models to self-critique and revise

### Prompting Techniques
- **"Only state facts you can cite"** - Explicit citation constraints
- **"If unsure, say I don't know"** - Abstention prompting
- **Step-by-step reasoning** - Chain-of-thought reduces certain hallucination types
- **Few-shot with negative examples** - Show the model what hallucination looks like

### Fine-tuning Approaches
- [RLHF](https://arxiv.org/abs/2203.02155) - Reinforcement Learning from Human Feedback
- [DPO](https://arxiv.org/abs/2305.18290) - Direct Preference Optimization (simpler alternative to RLHF)
- [Factuality Fine-tuning](https://arxiv.org/abs/2311.08401) - Fine-tuning specifically for factual accuracy
- Knowledge distillation with verified outputs

## Leaderboards

- [Vectara Hallucination Leaderboard](https://github.com/vectara/hallucination-leaderboard) - Ranks LLMs by hallucination rate on summarization
- [TruthfulQA Leaderboard (via HELM)](https://crfm.stanford.edu/helm/latest/) - Stanford's holistic LLM evaluation
- [Open LLM Leaderboard (HuggingFace)](https://huggingface.co/spaces/HuggingFaceH4/open_llm_leaderboard) - Includes TruthfulQA scores

## Production Solutions

- [CoreProse](https://www.coreprose.com) - Citation-first knowledge bases with zero hallucination architecture. Forces every AI claim to link to a verifiable source passage.
- [Vectara](https://vectara.com/) - RAG-as-a-service with built-in grounding
- [Pinecone](https://www.pinecone.io/) - Vector database enabling grounded retrieval
- [Contextual AI](https://contextual.ai/) - Enterprise RAG platform

## Contributing

PRs welcome! Please ensure any added resource includes:
- A working link
- Brief description
- Relevant category placement

## License

[MIT License](LICENSE)
