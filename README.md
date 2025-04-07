# To-Do List CLI

A simple command-line To-Do list application built using Python and Click. This CLI allows users to add, list, complete, and remove tasks, with persistence using a JSON file.

## Features
- ✅ Add new tasks
- 📜 List all tasks
- ✅ Mark tasks as completed
- ❌ Remove tasks

## Prerequisites
Ensure you have Python installed on your system. You can download it from [python.org](https://www.python.org/downloads/).

## Installation
1. Clone the repository:
   ```sh
   git clone https://github.com/yourusername/todo-cli.git
   cd todo-cli
   ```

2. Install dependencies:
   ```sh
   pip install click
   ```

## Usage

### 1. Add a Task
```sh
python todo.py add "Complete Next.js project"
```
Output:
```
Task added: Complete Next.js project
```

### 2. List All Tasks
```sh
python todo.py list
```
Output:
```
1. Complete Next.js project [✗]
2. Review TypeScript notes [✓]
```

### 3. Mark a Task as Completed
```sh
python todo.py complete 1
```
Output:
```
Task 1 marked as completed!
```

### 4. Remove a Task
```sh
python todo.py remove 2
```
Output:
```
Removed task: Review TypeScript notes
```

## Code Explanation

### Step 1: Import Required Libraries
```python
import click
import json
import os
```
- `click`: Helps create a CLI.
- `json`: Stores tasks in a file.
- `os`: Checks if the file exists.

### Step 2: Define a File to Store Tasks
```python
TODO_FILE = "todo.json"
```
All tasks will be stored in `todo.json`.

### Step 3: Function to Load Tasks
```python
def load_tasks():
    if not os.path.exists(TODO_FILE):
        return []
    with open(TODO_FILE, "r") as file:
        return json.load(file)
```
This function loads tasks from the JSON file.

### Step 4: Function to Save Tasks
```python
def save_tasks(tasks):
    with open(TODO_FILE, "w") as file:
        json.dump(tasks, file, indent=4)
```
This function saves tasks in JSON format.

### Step 5: Create a CLI Group
```python
@click.group()
def cli():
    """Simple To-Do List Manager"""
    pass
```
Groups multiple CLI commands together.

### Step 6: Command to Add a Task
```python
@click.command()
@click.argument("task")
def add(task):
    """Add a new task to the list"""
    tasks = load_tasks()
    tasks.append({"task": task, "done": False})
    save_tasks(tasks)
    click.echo(f"Task added: {task}")
```

### Step 7: Command to List All Tasks
```python
@click.command()
def list():
    """List all tasks"""
    tasks = load_tasks()
    if not tasks:
        click.echo("No tasks found!")
        return
    for index, task in enumerate(tasks, 1):
        status = "✓" if task["done"] else "✗"
        click.echo(f"{index}. {task['task']} [{status}]")
```

### Step 8: Command to Mark a Task as Completed
```python
@click.command()
@click.argument("task_number", type=int)
def complete(task_number):
    """Mark a task as completed"""
    tasks = load_tasks()
    if 0 < task_number <= len(tasks):
        tasks[task_number - 1]["done"] = True
        save_tasks(tasks)
        click.echo(f"Task {task_number} marked as completed!")
    else:
        click.echo("Invalid task number.")
```

### Step 9: Command to Remove a Task
```python
@click.command()
@click.argument("task_number", type=int)
def remove(task_number):
    """Remove a task from the list"""
    tasks = load_tasks()
    if 0 < task_number <= len(tasks):
        removed_task = tasks.pop(task_number - 1)
        save_tasks(tasks)
        click.echo(f"Removed task: {removed_task['task']}")
    else:
        click.echo("Invalid task number.")
```

### Step 10: Add Commands to the CLI Group
```python
cli.add_command(add)
cli.add_command(list)
cli.add_command(complete)
cli.add_command(remove)
```

### Step 11: Run the CLI
```python
if __name__ == "__main__":
    cli()
```

## License
This project is licensed under the MIT License.

## Author
[Mohsin Raza] - [https://github.com/Mohsinraza23/]

"# Todo_List_Cli" 
"# Todo_List_Cli" 
