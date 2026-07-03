# TemarIA 📚🤖

> AI-powered study assistant for Spanish civil-service exams (*oposiciones*).
> Upload your official syllabus PDFs and get answers grounded in **your** temario — with exact citations — plus auto-generated practice tests.

## Why

Preparing for an oposición means digesting thousands of pages of dense legal and administrative text. Generic AI chatbots are unreliable study partners: they hallucinate article numbers and mix up regulations. **TemarIA only answers from the documents you upload**, using Retrieval-Augmented Generation (RAG), and every answer links back to the exact tema and page it came from.

## Features

**MVP (in progress)**
- [ ] PDF ingestion: parse, clean and split syllabus documents into semantic chunks
- [ ] Vector search over your temario (PostgreSQL + pgvector)
- [ ] Grounded Q&A with source citations (tema + page)
- [ ] Practice-test generation: multiple-choice questions from any chosen tema

**Roadmap**
- [ ] Minimal web UI
- [ ] Spaced-repetition review of failed questions
- [ ] Study-progress dashboard
- [ ] Multi-syllabus support

## Tech stack

| Layer | Choice |
|---|---|
| Language | Java 21 |
| Framework | Spring Boot 3 + Spring AI |
| Vector store | PostgreSQL + pgvector |
| LLM & embeddings | Provider-agnostic via Spring AI (Gemini / Claude / OpenAI) |
| Infra | Docker Compose |
| Tests | JUnit 5, Mockito |

## Architecture

```
 PDF ──▶ parser ──▶ chunker ──▶ embeddings ──▶ pgvector
                                                  │
 question ──▶ embedding ──▶ similarity search ────┤
                                                  ▼
                                     LLM ──▶ answer + citations
```

## Getting started

> 🚧 Under active development — instructions will evolve with each milestone.

```bash
# 1. Start the database
docker compose up -d

# 2. Set your LLM provider key
export SPRING_AI_OPENAI_API_KEY=your-key   # or the Gemini / Anthropic equivalent

# 3. Run
./mvnw spring-boot:run
```

## Milestones

- **M0 — Console MVP:** ingest one PDF, ask one question, get a cited answer
- **M1 — REST API:** Spring Boot endpoints with unit tests
- **M2 — Web UI:** minimal front end to chat with your temario
- **M3 — Deployment:** public demo instance

## Author

**Borja Pardo** — backend developer (Java / Spring) based in Valencia, Spain.
[LinkedIn](https://www.linkedin.com/in/borja-pardo-juanes-130973335/) · [GitHub](https://github.com/CalvaryBloom)

## License

MIT
