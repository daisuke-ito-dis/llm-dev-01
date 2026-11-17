FROM ghcr.io/open-webui/open-webui:ollama
ARG MODEL=hf.co/bartowski/Qwen2.5-1.5B-Instruct-GGUF:Q4_K_M
ENV MODEL=${MODEL} \
    OLLAMA_MODELS=/opt/ollama/models \
    HOME=/tmp/home \
    DATA_DIR=/tmp/data \
    DEFAULT_MODELS=${MODEL} \
    WEBUI_AUTH=False \
    ENABLE_OPENAI_API=False
RUN mkdir -p $OLLAMA_MODELS $HOME $DATA_DIR && \
    bash -c 'ollama serve & \
    until ollama list >/dev/null 2>&1; do sleep 1; done; \
    ollama pull "$MODEL"; \
    kill %1' && \
    chgrp -R 0 /opt/ollama /tmp/home /tmp/data /app/backend && \
    chmod -R g=u /opt/ollama /tmp/home /tmp/data /app/backend
