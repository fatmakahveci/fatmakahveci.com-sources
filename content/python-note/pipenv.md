---
title: Pipenv
description: Pipenv
summary: "Updated by Fatma, Mar 28, 2023."
date: 28-03-2023
categories:
  - "Coding"
tags:
  - "python"
  - "coding"
  - "algorithms"
  - "data structures"
comments: true
---
- They are isolated containers containing all the software dependencies for a given project.
- You should use a dedicated virtual environment for each new Python project.
- Historically Python developers have used either `virtualenv` or `pyenv` to configure the virtual environment, but prominent Python developer Kenneth Reitz released `Pipenv` which is now the officially recommended Python packaging tool.
- Pipenv creates a `Pipfile` containing software dependencies and a `Pipfile.lock` for ensuring deterministic builds.
  - Determinism means that every time you download the software in a new virtual environment, you will have the same configuration.
