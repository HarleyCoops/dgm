<h1 align="center">
    Darwin Gödel Machine:<br/>Open-Ended Evolution of Self-Improving Agents
</h1>

<p align="center">
  <a href="https://github.com/jennyzzt/dgm/blob/main/LICENSE"><img src="https://img.shields.io/badge/License-Apache%202.0-blue.svg?style=for-the-badge"></a>
  <a href="https://arxiv.org/abs/2505.22954"><img src="https://img.shields.io/badge/arXiv-2505.22954-b31b1b.svg?logo=arxiv&style=for-the-badge"></a>
  <a href="https://sakana.ai/dgm/"><img src="https://img.shields.io/badge/-Blog-%238D6748?style=for-the-badge&logo=Website&logoColor=white"></a>
  <a href="https://x.com/SakanaAILabs/status/1928272612431646943"><img src="https://img.shields.io/badge/twitter-%230077B5.svg?&style=for-the-badge&logo=twitter&logoColor=white&color=00acee"></a>
  <a href="https://drive.google.com/drive/folders/1Kcu9TbIa9Z50pJ7S6hH9omzzD1pxIYZC?usp=sharing"><img src="https://img.shields.io/badge/Experiment%20Logs-4285F4?style=for-the-badge&logo=googledrive&logoColor=white"></a>
</p>

<p align="center">
  <img src="./misc/overview.gif" width="100%" height="auto" />
</p>

Repository for **Darwin Gödel Machine (DGM)**, a novel self-improving system that iteratively modifies its own code (thereby also improving its ability to modify its own codebase) and empirically validates each change using coding benchmarks.

<p align="center">
<img src="./misc/conceptual.svg"/></a><br>
</p>


## Setup
```bash
# API keys, add to ~/.bashrc
export OPENAI_API_KEY='...'
export ANTHROPIC_API_KEY='...'
```

```bash
# Verify that Docker is properly configured in your environment.
docker run hello-world
 
# If a permission error occurs, add the user to the Docker group
sudo usermod -aG docker $USER
newgrp docker
```

```bash
# Install dependencies
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt

# Optional: for running analysis
sudo apt-get install graphviz graphviz-dev
pip install -r requirements_dev.txt
```

> **If you're on Windows Subsystem for Linux (WSL)**, first install Python venv support and create a virtual environment:
>
> ```bash
> sudo apt update
> sudo apt install python3-venv
> python3 -m venv .venv
> source .venv/bin/activate
> pip install --upgrade pip
> ```

```bash
# Clone SWE-bench
cd swe_bench
git clone https://github.com/princeton-nlp/SWE-bench.git
cd SWE-bench
git checkout dc4c087c2b9e4cefebf2e3d201d27e36
pip install -e .
cd ../../

# Prepare Polyglot
# Make sure git is properly configured in your environment with username and email
python polyglot/prepare_polyglot_dataset.py
```

## Running the DGM
```bash
python DGM_outer.py
```
By default, outputs will be saved in the `output_dgm/` directory.

## File Structure
- `analysis/` scripts used for plotting and analysis
- `initial/` SWE-bench logs and performance of the initial agent
- `initial_polyglot/` Polyglot logs and performance of the initial agent
- `swe_bench/` code needed for SWE-bench evaluation
- `polyglot/` code needed for Polyglot evaluation
- `prompts/` prompts used for foundation models
- `tests/` tests for the DGM system
- `tools/` tools available to the foundation models
- `coding_agent.py` main implementation of the initial coding agent
- `DGM_outer.py` entry point for running the DGM algorithm

## Defining Custom Agents and Tasks

The DGM framework is extensible and allows you to define your own agents and tasks. Here's how:

### Creating Custom Tasks

1. **Simple Task List**: Create a JSON file with task IDs:
```json
// custom_tasks/subsets/small.json
[
    "task-001",
    "task-002",
    "task-003"
]
```

2. **Full Task Dataset**: Create a dataset loader with detailed task structure:
```python
# custom_tasks/dataset.py
def load_custom_dataset():
    return [
        {
            "instance_id": "task-001",
            "problem_statement": "Write a function that sorts a list",
            "base_commit": "initial",
            "test_patch": "def test_sort():\n    assert sort([3,1,2]) == [1,2,3]",
            "patch": "def sort(lst):\n    return sorted(lst)"  # Optional gold solution
        }
    ]
```

### Creating Custom Agents

**Option A - Extend Existing Agent**:
```python
# my_custom_agent.py
from coding_agent import AgenticSystem

class CustomAgenticSystem(AgenticSystem):
    def forward(self):
        """Override with custom problem-solving logic"""
        instruction = f"""
        Custom instructions for: {self.problem_statement}
        Use specialized techniques...
        """
        from llm_withtools import chat_with_agent
        return chat_with_agent(instruction, model=self.code_model, 
                              msg_history=[], logging=safe_log)
```

**Option B - New Agent Architecture**:
```python
class AlternativeAgent:
    def __init__(self, problem_statement, git_tempdir, **kwargs):
        self.problem_statement = problem_statement
        self.git_tempdir = git_tempdir
    
    def solve(self):
        # Implement custom solving strategy
        pass
```

### Integration Steps

1. **Create evaluation harness** in `custom_tasks/harness.py`
2. **Modify DGM_outer.py** to load your dataset:
```python
if args.custom_tasks:
    from custom_tasks.dataset import load_custom_dataset
    dataset = load_custom_dataset()
```

3. **Run with custom setup**:
```bash
python DGM_outer.py --custom_tasks --agent_type custom
```

### Example: Math Problem Solver

```python
# math_tasks/dataset.py
def load_math_dataset():
    return [{
        "instance_id": "math-001",
        "problem_statement": "Solve: 2x + 5 = 13",
        "test_patch": "assert solve_equation('2x + 5 = 13') == 4"
    }]

# math_agent.py  
class MathAgent(AgenticSystem):
    def forward(self):
        instruction = f"Solve step by step: {self.problem_statement}"
        # Agent solves math problems...
```

For detailed implementation examples and safety considerations, see the source code and inline documentation.

## Logs from Experiments
This [google drive folder](https://drive.google.com/drive/folders/1Kcu9TbIa9Z50pJ7S6hH9omzzD1pxIYZC?usp=sharing) contains all the foundation model output logs from the experiments shown in the paper.

## Safety Consideration
> [!WARNING]  
> This repository involves executing untrusted, model-generated code. We strongly advise users to be aware of the associated safety risks. While it is highly unlikely that such code will perform overtly malicious actions under our current settings and with the models we use, it may still behave destructively due to limitations in model capability or alignment. By using this repository, you acknowledge and accept these risks.

## Acknowledgement

The evaluation framework implementations are based on the [SWE-bench](https://github.com/swe-bench/SWE-bench) and [polyglot-benchmark](https://github.com/Aider-AI/polyglot-benchmark) repositories.

## Citing
If you find this project useful, please consider citing:
```bibtex
@article{zhang2025darwin,
  title={Darwin Godel Machine: Open-Ended Evolution of Self-Improving Agents},
  author={Zhang, Jenny and Hu, Shengran and Lu, Cong and Lange, Robert and Clune, Jeff},
  journal={arXiv preprint arXiv:2505.22954},
  year={2025}
}
```
