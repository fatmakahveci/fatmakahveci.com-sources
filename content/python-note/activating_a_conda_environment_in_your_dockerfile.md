---
title: Activating a Conda environment in your Dockerfile
description: Activating a Conda environment in your Dockerfile
summary: "Updated by Fatma, Mar 28, 2023."
date: 28-03-2023
categories:
  - "Coding"
tags:
  - "Python"
  - "coding"
  - "algorithms"
  - "data structures"
comments: true
---
```bash
#!/bin/bash --login
# --login ensures the bash configuration is loaded, enabling Conda

set -euo pipefail
conda activate myenv
exec python run.py
```

```dockerfile
FROM continuumio/miniconda3

WORKDIR /app

# Create the environment
COPY environment.yml .
RUN conda env create -f environment.yml

# Make RUN commands use the new environment
RUN echo "conda activate myenv" >> ~/.bashrc
SHELL ["/bin/bash", "--login", "-c"]

# Demonstrate the environment is activated
RUN echo "Make sure flask is installed:"
RUN python -c "import flask"

# The code to run when a container is started
COPY run.py entrypoint.sh .
ENTRYPOINT ["./entrypoint.sh"]
```

`docker build -t condatest .`

`docker run condatest`
