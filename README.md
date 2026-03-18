<div align="center">

# 🐚 Minishell

> *"As beautiful as a shell"*

A lightweight Unix shell implementation built from scratch in C — a 42 School project.

Language: C &nbsp;|&nbsp; School: 42 &nbsp;|&nbsp; Status: Completed &nbsp;|&nbsp; Norminette: passing

</div>

---

## 📖 Overview

**Minishell** is a minimal yet functional Unix shell written in C, developed as part of the 42 curriculum. The goal is to understand the inner workings of a shell by implementing core features from scratch — including command parsing, process management, redirections, pipes, and environment variable handling.

This project deepens understanding of how operating systems handle processes, file descriptors, and inter-process communication.

---

## ✨ Features

### Built-in Commands
| Command | Description |
|---------|-------------|
| `echo` | Print arguments to standard output (`-n` flag supported) |
| `cd` | Change current working directory |
| `pwd` | Print current working directory |
| `export` | Set environment variables |
| `unset` | Unset environment variables |
| `env` | Display all environment variables |
| `exit` | Exit the shell with an optional status code |

### Shell Features
- **Prompt display** — Shows a custom prompt while waiting for input
- **Command history** — Navigate previous commands with arrow keys
- **Pipes** `|` — Chain commands together with pipelines
- **Redirections**
  - `<` — Redirect input
  - `>` — Redirect output
  - `>>` — Append output
  - `<<` — Here-document (heredoc)
- **Environment variables** — Expand `$VAR` and `$?` (last exit status)
- **Single `'` and double `"` quotes** — Handle quoting rules per POSIX standard
- **Signal handling** — Proper `Ctrl+C`, `Ctrl+D`, `Ctrl+\` behavior

---

## 🛠️ Installation

### Requirements
- GCC or Clang
- GNU Make
- `readline` library

```bash
# On macOS (with Homebrew)
brew install readline

# On Ubuntu/Debian
sudo apt-get install libreadline-dev
```

### Build

```bash
git clone https://github.com/kamile-ikiz/minishell.git
cd minishell
make
```

### Clean

```bash
make clean    # Remove object files
make fclean   # Remove object files and binary
make re       # Rebuild everything
```

---

## 🚀 Usage

```bash
./minishell
```

Once launched, you can use it like a regular shell:

```bash
minimini1shell$ echo "Hello, World!"
Hello, World!

minimini1shell$ ls -la | grep ".c" | wc -l
42

minimini1shell$ cat < input.txt >> output.txt

minimini1shell$ export MY_VAR=42
minimini1shell$ echo $MY_VAR
42

minimini1shell$ exit
```

---

## 🏗️ Project Structure

```
minishell/
├── builtins/               # Built-in command implementations
├── execute/                # Command execution & pipes & redirections
├── extras/                 # Helper / utility functions
├── token_parse/            # Tokenization & parsing
├── libft/                  # Custom C library (libft)
├── main.c                  # Entry point
├── minishell.h             # Main header file
└── Makefile
```

---

## ⚙️ How It Works

```
Input String
     │
     ▼
  Tokenizer  (token_parse)
     │  tokenize() → t_token list
     ▼
  Pipe Splitter  (token_parse)
     │  split_tokens_by_pipe() → t_segment list
     ▼
  Parser  (token_parse)
     │  parse_input() → t_command list
     ▼
  Expander  (extras)
     │  expand_all_variables(), prepare_heredocs()
     ▼
  Executor  (execute)
     │  execute_command() → fork, execve, pipes, redirections
     ▼
  Output / Next Prompt
```

1. **token_parse** — Tokenizes raw input, splits by pipes into segments, then builds a linked list of `t_command` structs
2. **extras** — Handles environment variable expansion (`$VAR`, `$?`) and heredoc preparation
3. **execute** — Forks child processes, sets up pipes and redirections, and calls `execve`
4. **builtins** — Handles built-in commands directly without forking

---

## 🧪 Testing

You can test the shell manually against bash behavior:

```bash
# Compare outputs
bash -c "your_command_here"
./minishell
```

Some edge cases to verify:
- Empty commands and whitespace-only input
- Unclosed quotes
- Invalid redirections
- Chained pipes with failing commands
- `$?` after each command

---

## ⚠️ Known Limitations

- Does not support logical operators (`&&`, `||`)
- No wildcard/glob expansion (`*`)
- Not a fully POSIX-compliant shell

---

## 👥 Authors

<div align="center">

| | |
|---|---|
| **kikiz** | [GitHub →](https://github.com/kamile-ikiz) |
| **beysonme** | [GitHub →](https://github.com/besonmez) |

*Made with ☕ and existential dread at 42 Istanbul*

</div>

---

## 📚 Resources

- [GNU Bash Reference Manual](https://www.gnu.org/software/bash/manual/bash.html)
- [The Open Group — Shell Command Language](https://pubs.opengroup.org/onlinepubs/9699919799/utilities/V3_chap02.html)
- [`readline` Library Documentation](https://tiswww.case.edu/php/chet/readline/rltop.html)

## 💙 Special Thanks

A huge shoutout to our friends at **42 Istanbul** — the late-night debugging sessions, the *"wait, does yours segfault too?"* moments, and the endless peer reviews made this project so much more than just code. This shell was built with caffeine, curiosity, and a whole lot of support from the best campus community we could ask for. You know who you are. 🫶

---

<div align="center">
<sub>42 School Project — minishell</sub>
</div>
