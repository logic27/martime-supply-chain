# Meta PyTorch Hackathon Round 1

## What Round 1 is asking for

You need to build a real-world `OpenEnv` environment that an AI agent can interact with using:

- `reset()`
- `step()`
- `state()`

Your submission needs to include at least:

- A real-world task, not a toy game
- Full OpenEnv structure, including `openenv.yaml`
- Typed action and observation models
- At least 3 tasks with graders:
  - easy
  - medium
  - hard
- Scores in the `0.0` to `1.0` range
- A meaningful reward function with partial progress signals
- A root-level `inference.py`
- A working `Dockerfile`
- Deployment to Hugging Face Spaces
- A README with setup and environment details

## What the judges will check

Before deeper judging, they will verify:

- The Hugging Face Space responds and supports `reset()`
- Your environment follows the OpenEnv spec
- The Dockerfile builds
- `inference.py` runs successfully
- 3 or more tasks exist and graders return scores in `0.0` to `1.0`

They also mention these environment variables for inference:

- `API_BASE_URL`
- `MODEL_NAME`
- `HF_TOKEN`

They specifically require using the OpenAI client for LLM calls.

## Your current local status

Checked in this workspace on 2026-03-31:

- `python3 --version` -> `3.9.6`
- `pip3 --version` -> available
- `docker --version` -> not installed
- `uv --version` -> not installed

This means local development is not ready yet.

## Minimum local setup you should do first

### 1. Upgrade Python to 3.11+

OpenEnv docs list Python `3.11+` as a prerequisite.

If you use Homebrew on macOS:

```bash
brew install python@3.11
python3.11 --version
```

### 2. Install `uv`

OpenEnv docs recommend `uv` for dependency locking.

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
uv --version
```

### 3. Install Docker Desktop

Docker is required for:

- local container testing
- OpenEnv build/validate flow
- final submission readiness

After installing Docker Desktop, verify:

```bash
docker --version
docker ps
```

### 4. Create a project virtual environment

From this folder:

```bash
cd /Users/anmolkoul07/hail-mary
python3.11 -m venv .venv
source .venv/bin/activate
python --version
```

### 5. Install OpenEnv

The OpenEnv packaging guide shows installation from GitHub:

```bash
pip install --upgrade pip
pip install https://github.com/meta-pytorch/OpenEnv.git
openenv --help
```

### 6. Scaffold your environment

Once OpenEnv is installed:

```bash
openenv init my_env
```

That should generate a structure like:

```text
my_env/
├── __init__.py
├── README.md
├── client.py
├── models.py
├── openenv.yaml
├── pyproject.toml
├── uv.lock
└── server/
    ├── __init__.py
    ├── app.py
    ├── my_environment.py
    ├── requirements.txt
    └── Dockerfile
```

### 7. Run the basic local workflow

OpenEnv docs show this development loop:

```bash
openenv serve
openenv validate --verbose
openenv build
```

## Best way to start the project simply

Do not begin with the grader or Hugging Face deployment.

Start in this order:

1. Pick one real-world environment idea
2. Get `reset()`, `step()`, and `state()` working locally
3. Define action and observation models
4. Add one easy task
5. Add reward shaping
6. Expand to medium and hard tasks
7. Write `inference.py`
8. Validate and containerize
9. Deploy to Hugging Face Spaces

## Good Round 1 idea categories

Since games and toy tasks are discouraged, better directions are:

- customer support workflow simulator
- calendar scheduling assistant
- expense approval workflow
- email triage environment
- document review or form-filling workflow
- bug triage environment

## Recommended first milestone

A good first milestone for us is:

"Build one tiny real-world environment locally with one task, one reward signal, and a working `reset()/step()/state()` loop."

## Sources

- Scaler Round 1 dashboard: https://www.scaler.com/school-of-technology/meta-pytorch-hackathon/dashboard
- OpenEnv Building Environments: https://meta-pytorch.org/OpenEnv/auto_getting_started/plot_03_building_environments.html
- OpenEnv Packaging and Deploying: https://meta-pytorch.org/OpenEnv/auto_getting_started/environment-builder.html
