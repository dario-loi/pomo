# pomo

A fancy terminal-based [pomodoro](https://en.wikipedia.org/wiki/Pomodoro_Technique) timer.

It uses the [Typer](https://typer.tiangolo.com/) library to provide a pretty terminal based interface,
it also sends desktop notifications using [plyer](https://plyer.readthedocs.io/en/latest/). These
*should* work on both Linux, Windows, and MacOS.


![pomo](carbon.png)
*The pomo timer in action*

## Installation

You can install the package using `pdm` in a fairly simple and straightforward way:

```bash
git clone https://github.com/dario-loi/pomo.git
cd pomo
pdm install
```

You can install the required dependencies with `pip` (with the help of `pdm`) in this way:

```bash
pdm export -f requirements.txt | pip install -r /dev/stdin
```

You can then move/symlink the `pomo` script to a directory in your `$PATH` (e.g. `/usr/local/bin`).

## Usage

Running the command `pomo --help` will show you the available options, this is quite detailed thanks to `Typer`:

```zsh
❯ pomo --help
                                                                                                                                                                              
 Usage: pomo [OPTIONS] [DURATION] [TASK_NAME] [BREAK_TIME]                                                                                                                    
                                                                                                                                                                              
 Start the Pomodoro timer.                                                                                                                                                    
                                                                                                                                                                              
╭─ Arguments ────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╮
│   duration        [DURATION]    Duration of the Pomodoro session in minutes. [default: 25]                                                                                 │
│   task_name       [TASK_NAME]   Name of the task for the Pomodoro session. [default: Pomodoro]                                                                             │
│   break_time      [BREAK_TIME]  Break time between Pomodoro sessions in minutes. [default: 5]                                                                              │
╰────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯
╭─ Options ──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╮
│ --loop                                                         If provided, restart the Pomodoro timer automatically after each session.                                   │
│ --version             -v                                       Show the version and exit.                                                                                  │
│ --install-completion          [bash|zsh|fish|powershell|pwsh]  Install completion for the specified shell. [default: None]                                                 │
│ --show-completion             [bash|zsh|fish|powershell|pwsh]  Show completion for the specified shell, to copy it or customize the installation. [default: None]          │
│ --help                                                         Show this message and exit.                                                                                 │
╰────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯
```