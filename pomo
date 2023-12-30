#!/usr/bin/env python3

import typer
import time
from datetime import datetime, timedelta
from rich.progress import Progress
from plyer import notification

app = typer.Typer(no_args_is_help=True)


def pomodoro_timer(
    duration_minutes: int,
    task_name: str = "Pomodoro",
    break_time: int = 5,
    loop: bool = False,
):
    """
    Start a Pomodoro timer.

    :param duration_minutes: Duration of the Pomodoro session in minutes.
    :param task_name: Name of the task for the Pomodoro session.
    :param break_time: Mandatory break time between Pomodoro sessions in minutes.
    :param loop: If provided, restart the Pomodoro timer automatically after each session.
    """

    t_unit = "minutes" if duration_minutes != 1 else "minute"

    while True:
        # Pomodoro session
        typer.echo(
                f"🍅 Pomodoro Timer: {duration_minutes} {t_unit} for task '{task_name}'"
        )
        notification.notify(
                        title = f"Pomodoro Timer",
                        message = f"⏳ Starting {duration_minutes} {t_unit} timer for task '{task_name}'",
                        timeout = 15,
                    )

        start_time = datetime.now()
        end_time = start_time + timedelta(minutes=duration_minutes)

        with Progress() as progress:
            task = progress.add_task(
                f"[cyan]Progress - {task_name}...", total=duration_minutes * 60
            )

            while not progress.finished:
                elapsed_time = datetime.now() - start_time
                progress.update(task, completed=elapsed_time.total_seconds())
                time.sleep(1)

                if datetime.now() >= end_time:
                    progress.stop()
                    typer.echo(f"\n🎉 {task_name} completed!")
                    progress.update(task, completed = (end_time - start_time).total_seconds())
                    notification.notify(
                        title = f"Pomodoro Timer",
                        message = f'{task_name} completed!\nTaking a {break_time}-minute break...',
                        timeout = 15,
                    )
                    break

        # Break time
        typer.echo(f"\n⏳ Taking a {break_time}-minute break...")
        start_time = datetime.now()
        end_time = start_time + timedelta(minutes=break_time)

        with Progress() as progress:
            task = progress.add_task("[cyan]Break Progress...", total=break_time * 60)

            while not progress.finished:
                elapsed_time = datetime.now() - start_time
                progress.update(task, completed=elapsed_time.total_seconds())
                time.sleep(1)

                if datetime.now() >= end_time:
                    progress.stop()
                    typer.echo("\n🍵 Break time completed!")
                    progress.update(task, completed = (end_time - start_time).total_seconds())
                    break

        if not loop:
            return
        

def print_version(value: bool):
    if value:
        typer.echo("Pomodoro Timer v1.0.0")
        raise typer.Exit()


@app.command()
def start(
    duration: int = typer.Argument(
        25, help="Duration of the Pomodoro session in minutes."
    ),
    task_name: str = typer.Argument(
        "Pomodoro", help="Name of the task for the Pomodoro session."
    ),
    break_time: int = typer.Argument(
        5, help="Break time between Pomodoro sessions in minutes."
    ),
    loop: bool = typer.Option(
        False,
        "--loop",
        help="If provided, restart the Pomodoro timer automatically after each session.",
    ),
    version: bool = typer.Option(
        None,
        "--version",
        "-v",
        callback=print_version,
        is_eager=True,
        help="Show the version and exit.",
    ),
):
    """Start the Pomodoro timer."""
    
    assert duration > 0, "Duration must be greater than 0."
    assert break_time >= 0, "Break time must be a positive number."
    
    pomodoro_timer(duration, task_name, break_time, loop)


if __name__ == "__main__":
    app()
