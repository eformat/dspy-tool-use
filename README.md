# dspy demos

[DSPy](https://dspy.ai/) -"Programming - not prompting - LMs"

## setup

Python

```bash
python3.12 -m venv venv
source venv/bin/activate

pip install --upgrade --quiet \
  mlflow \
  ipykernel \
  rich \
  dspy \
  ujson \
  openai
```

MLFLow

```bash
mlflow ui --port 5500 &
```

LLM's locally

```bash
export MODEL=DeepSeek-R1-0528-Qwen3-8B-Q4_K_M.gguf
export MODEL=Llama-3.2-3B-Instruct-Q8_0.gguf

podman run -p 8080:8080 --net=host --device nvidia.com/gpu=0 --security-opt label=type:nvidia_container_t -v /home/mike/instructlab/models:/models:Z ghcr.io/ggerganov/llama.cpp:full-cuda --server -m /models/${MODEL} --gpu-layers 999 -np 3 --ctx-size 18000
```

LLM's remotely

```bash
oc -n llama-serving port-forward svc/sno-granite32-vllm-predictor-00001-private 8080:80 &
oc -n llama-serving port-forward svc/sno-llama32-vllm-predictor-00001-private 8080:80 &
```

Run notebooks in vscode - `code .`
