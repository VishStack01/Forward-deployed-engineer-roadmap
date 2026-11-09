# Portfolio project ideas for Forward Deployed Engineers

Three shipped systems with honest write-ups beat ten tutorials. Pick projects that look like client work: real data, a measurable result, deployed somewhere a reviewer can try it.

## What every portfolio project needs

1. A one-paragraph problem statement written for a non-engineer
2. A live URL or a 2-minute screen recording
3. An evaluation: a small test set and the numbers, before and after your best change
4. Cost and latency per request
5. A short "what I'd do next" section; reviewers read this first

## 25 project ideas

| # | Project | What you build | Start from | Fit |
| --- | --- | --- | --- | --- |
| 1 | Autonomous Multi-Agent Enterprise Swarm | A network of specialized agents on LangGraph that coordinates corporate workflows with self-correcting loops. | [langchain-ai/langgraph](https://github.com/langchain-ai/langgraph) | Core FDE |
| 2 | Custom-Trained 7B Model Factory | A pipeline that automates continuous domain adaptation with QLoRA on curated industry data. | [axolotl-ai-cloud/axolotl](https://github.com/axolotl-ai-cloud/axolotl) | Strong fit |
| 3 | Real-Time Low-Latency Audio Translator | A streaming voice pipeline using optimized Whisper plus voice synthesis. | [openai/whisper](https://github.com/openai/whisper) | Strong fit |
| 4 | Automated LLM Evaluation Suite | A CI benchmarking platform that tests models against security edge cases and hallucination. | [truera/trulens](https://github.com/truera/trulens) | Core FDE |
| 5 | Petabyte-Scale Vector Search Engine | An optimized vector index supporting sub-10ms semantic search. | [qdrant/qdrant](https://github.com/qdrant/qdrant) | Strong fit |
| 6 | Private Hybrid-RAG Enterprise Knowledge Graph | Secure enterprise search mapping graph structure alongside vector embeddings. | [run-llama/llama_index](https://github.com/run-llama/llama_index) | Core FDE |
| 7 | Self-Hosted vLLM Engine Cluster | Autoscaling GPU serving tuned for real-time token throughput. | [vllm-project/vllm](https://github.com/vllm-project/vllm) | Strong fit |
| 8 | Vision-Language Model Quality Inspector | Edge machine vision that flags manufacturing defects on an assembly line. | [haotian-liu/LLaVA](https://github.com/haotian-liu/LLaVA) | Strong fit |
| 9 | Predictive Hardware Failure Monitor | Anomaly detection over real-time data-center telemetry. | [prometheus/prometheus](https://github.com/prometheus/prometheus) | beyond |
| 10 | Local Edge AI Smart Gateway | A compressed small language model running fully offline. | [ollama/ollama](https://github.com/ollama/ollama) | Core FDE |
| 11 | Distributed Relational Key-Value Store | An ACID distributed transactional database built on Raft consensus. | [tikv/tikv](https://github.com/tikv/tikv) | beyond |
| 12 | High-Throughput Financial Matching Engine | An ultra-low-latency order matching platform under strict SLAs. | [exchange-core/exchange-core](https://github.com/exchange-core/exchange-core) | beyond |
| 13 | Global CDN Edge Router | An edge proxy handling dynamic topology, caching, and TLS termination. | [envoyproxy/envoy](https://github.com/envoyproxy/envoy) | beyond |
| 14 | Distributed Job Scheduler Engine | Fault-tolerant orchestration that preserves state through infrastructure crashes. | [temporalio/temporal](https://github.com/temporalio/temporal) | Strong fit |
| 15 | Custom Service Mesh Sidecar Proxy | A sidecar that injects mutual TLS and exports detailed telemetry. | [istio/istio](https://github.com/istio/istio) | beyond |
| 16 | Real-Time Event Streaming Broker | A clustered append-only log with atomic partition delivery. | [redpanda-data/redpanda](https://github.com/redpanda-data/redpanda) | beyond |
| 17 | API Gateway with Dynamic Token Filters | A cloud-native rate-limiting gateway backed by distributed state. | [kong/kong](https://github.com/kong/kong) | Core FDE |
| 18 | Distributed Erasure-Coded Object Storage | Fault-tolerant object storage spreading blocks across commodity clusters. | [seaweedfs/seaweedfs](https://github.com/seaweedfs/seaweedfs) | beyond |
| 19 | Zero-Downtime Database Migration Engine | Changes live table schemas at scale without blocking writes. | [github/gh-ost](https://github.com/github/gh-ost) | Strong fit |
| 20 | Multi-Region WireGuard VPN | A secure overlay network joining virtual private clouds across continents. | [WireGuard/wireguard-go](https://github.com/WireGuard/wireguard-go) | beyond |
| 21 | Legacy Mainframe Event-Driven Data Bridge | An integration bus streaming legacy database changes into Kafka topics. | [debezium/debezium](https://github.com/debezium/debezium) | Core FDE |
| 22 | Industrial IoT Predictive Anomaly Engine | An edge analytics gateway feeding a central time-series store. | [timescale/timescaledb](https://github.com/timescale/timescaledb) | Strong fit |
| 23 | Cross-Enterprise Supply Chain Simulator | Graph analytics over shipping lanes that predicts disruptions and reroutes. | [neo4j/neo4j](https://github.com/neo4j/neo4j) | Strong fit |
| 24 | Air-Gapped Sovereign Cloud AI Platform | Isolated infrastructure running private LLMs inside a compliance perimeter. | [kubeflow/kubeflow](https://github.com/kubeflow/kubeflow) | Core FDE |
| 25 | Automated Risk Underwriting Pipeline | Document parsing that extracts structure from unstructured financial records. | [deepset-ai/haystack](https://github.com/deepset-ai/haystack) | Core FDE |

25 more ideas, with build plans and how each maps to FDE interview questions, are in the project bank inside [Zero to FDE](https://zero-to-fde-90-days.site/forward-deployed-engineer-program?utm_source=github&utm_medium=referral&utm_campaign=roadmap_repo&utm_content=projects).
