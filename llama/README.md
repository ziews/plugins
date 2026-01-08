# Llama Plugin

Local LLM inference via [llama.cpp](https://github.com/ggerganov/llama.cpp).

## Installation

### 1. Install llama.cpp

```bash
git clone https://github.com/ggerganov/llama.cpp
cd llama.cpp
cmake -B build
cmake --build build
sudo cmake --install build
```

### 2. Build Ziew with AI support

```bash
zig build -Dai=true
```

### 3. Add a model

Place any `.gguf` model file in `~/.ziew/models/`:

```bash
mkdir -p ~/.ziew/models
# Download a model (example: TinyLlama 1.1B)
wget -O ~/.ziew/models/tinyllama.gguf \
  https://huggingface.co/TheBloke/TinyLlama-1.1B-Chat-v1.0-GGUF/resolve/main/tinyllama-1.1b-chat-v1.0.Q4_K_M.gguf
```

## Recommended Models

| Model | Size | Best For |
|-------|------|----------|
| TinyLlama 1.1B | ~600MB | Testing, simple tasks |
| Llama 3.2 1B | ~700MB | General purpose |
| Phi-3 mini 3.8B | ~2GB | Best quality |

## Usage

### JavaScript API

```javascript
// One-shot completion
const response = await ziew.ai.complete('What is 2+2?');

// Streaming (recommended for longer responses)
for await (const token of ziew.ai.stream('Tell me a story')) {
  output.textContent += token;
}

// List available models
const models = await ziew.ai.models();
```

### Options

```javascript
// With options
for await (const token of ziew.ai.stream(prompt, {
  maxTokens: 256,  // Default: 256
})) {
  // ...
}
```

## Example: Chatbot

See `examples/chatbot/` for a complete local chatbot example with:
- Streaming responses
- Loading spinner
- Auto-detection of models from `~/.ziew/models/`

```bash
# Build and run
zig build -Dai=true chatbot
LD_LIBRARY_PATH=/usr/local/lib ./zig-out/bin/chatbot
```

## Model Storage

All models are stored in `~/.ziew/models/`. This is shared across all Ziew apps - download once, use everywhere.

```
~/.ziew/
└── models/
    ├── tinyllama.gguf
    ├── phi-3-mini.gguf
    └── ...
```

## Links

- [llama.cpp](https://github.com/ggerganov/llama.cpp)
- [HuggingFace Models](https://huggingface.co/models?library=gguf)
- [Ziew Documentation](https://ziew.sh/docs)
