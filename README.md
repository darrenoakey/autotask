![](banner.jpg)

# AutoTask

A multi-stage AI task orchestration tool that automatically executes complex programming tasks through iterative refinement using multiple AI providers.

## Purpose

AutoTask breaks down complex programming requests into multiple stages (perform, check, cleanup, test, commit, verify) and automatically retries until the task is successfully completed. It coordinates between different AI providers (Claude, Gemini) to ensure robust task completion with built-in verification and git integration.

## Installation

Ensure you have the following CLI tools installed and available in your PATH:
- `claude` - Claude CLI tool
- `gemini` - Google Gemini CLI tool
- `git` - For repository operations

Optional dependency:
```bash
pip install colorama  # For colored terminal output
```

## Usage

### Basic Command

```bash
./autotask "Your task description here"
```

### From File

```bash
./autotask --task-file path/to/task.txt
```

### Options

- `--providers` - Comma-separated list of providers to use (default: "claude,gemini")
- `--max-rounds` - Maximum number of retry attempts (default: 5)

## Examples

### Simple Task
```bash
./autotask "Create a Python function that calculates fibonacci numbers"
```

### Complex Refactoring
```bash
./autotask "Refactor the authentication module to use JWT tokens instead of sessions"
```

### Using Specific Providers
```bash
./autotask --providers claude "Fix the memory leak in the image processing function"
```

### From Task File with Multiple Rounds
```bash
./autotask --task-file complex_feature.txt --max-rounds 10
```

## Task Files

For complex multi-line task descriptions, create a `.task` file:

```text
Implement a REST API for user management with the following endpoints:
- POST /users - Create new user
- GET /users/:id - Get user by ID
- PUT /users/:id - Update user
- DELETE /users/:id - Delete user

Include proper error handling and validation.
```

Then run:
```bash
./autotask --task-file user_api.task
```

## Output

AutoTask creates a `work/` directory containing:
- Timestamped attempts for each run
- Stage-by-stage prompts and outputs
- Generated guides for iterative improvement
- Final verification results

## Workflow Stages

1. **Perform** - Initial task execution
2. **Check & Fix** - Error detection and correction
3. **Cleanup** - Code quality improvements
4. **Test** - Run and verify tests
5. **Commit** - Git commit with descriptive message
6. **Verify** - Final validation against requirements

The tool automatically retries if verification fails, using learnings from previous attempts.

## License

This project is licensed under [CC BY-NC 4.0](https://darren-static.waft.dev) - free to use and modify, but no commercial use without permission.
