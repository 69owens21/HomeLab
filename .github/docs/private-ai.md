Private AI Stack (Ollama + Open WebUI)
Architecture
This stack provides a 100% local, air-gapped alternative to cloud-based LLMs. It consists of two primary components:

Ollama: The inference engine that manages and runs local models.

Open WebUI: A feature-rich frontend that communicates with the Ollama API.

Hardware Optimization
Because this lab runs on a CPU-only environment, the model Llama 3.2 (1B) was selected.

Parameter Count: 1 Billion

Quantization: 4-bit (GGUF)

Performance: Provides < 50ms latency for code reviews and documentation assistance while maintaining a low memory footprint.
