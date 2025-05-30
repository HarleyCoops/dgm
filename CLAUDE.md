# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

### Running Tests
```bash
# Run all tests
pytest

# Run specific test file
pytest tests/test_bash_tool.py

# Run specific test
pytest tests/test_edit_tool.py::test_edit_tool_basic
```

### Running the Darwin Gödel Machine
```bash
# Basic run
python DGM_outer.py

# Run with custom parameters
python DGM_outer.py --max_generation 10 --selfimprove_size 4 --selfimprove_workers 2

# Run with Polyglot benchmark instead of SWE-bench
python DGM_outer.py --polyglot

# Continue from previous run
python DGM_outer.py --continue_from output_dgm/previous_run_id
```

### Evaluation Commands
```bash
# Run SWE-bench evaluation
python swe_bench/harness.py --predictions path/to/predictions.json --dataset swe_bench/subsets/small.json

# Run Polyglot evaluation  
python polyglot/run_evaluation.py --predictions path/to/predictions.json --subset small
```

## Architecture Overview

The Darwin Gödel Machine (DGM) is a self-improving system that iteratively modifies its own code and validates changes using coding benchmarks. The system has three main components:

### 1. Self-Improvement Loop (`DGM_outer.py`)
The outer loop that orchestrates the evolutionary process:
- Maintains an **archive** of agent versions
- Selects parent agents for mutation based on performance
- Runs multiple self-improvement attempts in parallel
- Evaluates modified agents on coding benchmarks
- Updates the archive with successful improvements

Key parameters:
- `max_generation`: Number of evolution cycles
- `selfimprove_size`: Number of parallel improvement attempts per generation
- `choose_selfimproves_method`: Parent selection strategy (random, score_prop, score_child_prop)

### 2. Coding Agent (`coding_agent.py`)
The inner agent that solves coding problems:
- Uses LLMs with tools (file editing, bash commands, etc.)
- Maintains conversation history in markdown logs
- Applies patches to codebases and runs tests
- Two modes: solving external problems or self-improvement

The agent uses these tools from `tools/`:
- `bash.py`: Execute shell commands
- `edit.py`: Make precise file edits

### 3. Self-Improvement Step (`self_improve_step.py`)
Executes a single self-improvement attempt:
- Diagnoses weaknesses using past evaluation logs
- Proposes code modifications to `coding_agent.py`
- Tests changes on sample problems
- Evaluates on larger benchmark subsets if initial tests pass

The process uses a multi-stage evaluation:
1. Small subset (quick validation)
2. Medium subset (if small passes threshold)
3. Full benchmark (if medium shows significant improvement)

## Key Design Patterns

### Containerized Evaluation
All code execution happens inside Docker containers for safety and reproducibility. The system:
- Builds custom Docker images for each benchmark problem
- Copies agent code into containers
- Captures all outputs and logs
- Implements timeouts to prevent hanging

### Performance Tracking
Each agent version stores metadata including:
- Parent lineage
- Performance scores on benchmarks
- Code modifications made
- Evaluation logs

### Prompt System
Prompts in `prompts/` are Python functions that dynamically construct prompts based on:
- Current agent code
- Past performance data
- Specific improvement objectives

## Working with the Codebase

### Adding New Benchmarks
1. Create dataset loader in appropriate directory (`swe_bench/` or `polyglot/`)
2. Implement harness for running evaluations
3. Add subset configurations (small/medium/large)

### Modifying the Agent
When working on `coding_agent.py`:
- Preserve the main `AgenticSystem` class interface
- Maintain compatibility with the tool system
- Ensure changes are testable in isolation

### Debugging Runs
- Check `output_dgm/*/dgm_outer.log` for high-level progress
- Individual agent attempts logged in `output_dgm/*/commit_id/*.md`
- Docker logs available in `*_docker.log` files