# https://blog.ianpreston.ca/conda/python/bash/2020/05/13/conda_envs.html

.ONESHELL:

SHELL=/bin/bash
CONDA_ACTIVATE=source $$(conda info --base)/etc/profile.d/conda.sh ; conda activate ; conda activate

help:
	@echo "- conda-update: Create conda environment {{cookiecutter.project}} with Python={{cookiecutter.python_version}} & pip-tools"
	@echo "- pip-tools: Compiles exact pip packages"
	@echo "- install: Creates conda environment & installs required packages using pip-tools"
	@echo "- setup: Initialize GIT & install pre-commit packages"
	@echo "- clean: Cleans up pycache & ipynb checkpoints"

conda-update:
	mamba env update --prune -f environment.yaml

pip-tools:
	$(CONDA_ACTIVATE) {{cookiecutter.conda_env_name}}
	pip install pip-tools
	pip-compile requirements/prod.in && pip-compile requirements/dev.in
	pip-sync requirements/prod.txt requirements/dev.txt

install: conda-update pip-tools

setup:
	$(CONDA_ACTIVATE) {{cookiecutter.conda_env_name}}
	git init
	pre-commit install

clean:
	rm -rf **/.ipynb_checkpoints **/.pytest_cache **/__pycache__ **/**/__pycache__ .ipynb_checkpoints .pytest_cache