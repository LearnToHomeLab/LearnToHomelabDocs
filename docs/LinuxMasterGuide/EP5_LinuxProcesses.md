# Linux Processes Tutorial 2025

<div style="display: flex; justify-content: center; align-items: center; height: 100%;">
    <iframe width="560" height="315" src="https://www.youtube.com/embed/0PWdJY-MgGQ?si=5GKgo4N2cuwiwYz7" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

## 1 ps (Processes)

The `ps` command shows a snapshot of currently running processes. It lists details like process ID (PID), user, CPU and memory usage, status, and command.

```
ps aux
```

- `a` shows processes for all users
- `u` adds detailed info (user, CPU%, MEM%)
- `x` shows processes without a controlling terminal

## 2. Controlling Terminal

A controlling terminal (TTY) is a terminal device associated with a process. Many processes run without a TTY, especially daemons or background jobs.

- **ps**: Shows information about running processes.
- **-e**: Lists _all_ Processes on the system (not just those belonging to the current user).
- **-o pid,tty,cmd**: Customizes the output columns to show:
- **pid**: Process ID — a unique number for each running process.
- **tty**: Terminal associated with the process (shows which terminal, if any, started the process).
- **cmd**: Command line that started the process.

```
ps -eo pid,tty,cmd
```

This shows each process with its PID, associated terminal (if any), and the command.

## 3. Process Details

Processes have attributes like PID, parent PID (PPID), status, CPU time, and command name. The `ps` command can display these with specific formatting:

- **ps**: Displays information about active processes.
- **-e**: Shows all processes on the system, not just those belonging to the current user or terminal.
- **-o**: Specifies the output format (which columns to display).

The list after `-o` defines which columns you’ll see:

- **pid**: Process ID — the unique number for each running process.
- **ppid**: Parent Process ID — shows which process started (is the parent of) this one.
- **stat**: Process status — displays the state of the process (e.g., running, sleeping, stopped) along with additional flags (like if it’s a foreground process).
- **cmd**: Command — shows the command used to start the process, including its arguments

```
ps -eo pid,ppid,stat,cmd
```

- `STAT` shows process state codes (e.g., S = sleeping, R = running).

## 4. Process Creation

Processes are created when a parent process forks a child. Common shells or applications spawn new processes. You can observe new processes appearing by running:

```
ps aux --sort=start_time | tail -10
```

This shows the 10 most recently started processes.

## 5. Process Termination

Processes can end normally or be terminated by signals. A terminated process is removed from the process table. You can kill a process by PID (next topic).

## 6. Signals

Signals are notifications sent to processes to trigger actions like stop, continue, or terminate. Common signals include:

- `SIGTERM` (signal 15) — polite termination request
- `SIGKILL` (signal 9) — forceful termination
- `SIGSTOP` (signal 19) — suspend process
- `SIGCONT` (signal 18) — resume process

Send a signal using `kill`:

```
kill -<SIGTERM number> <pid>
```

## 7. kill (Terminate)

Use `kill` to send signals to processes. The default signal is SIGTERM. To force kill:

```
kill -9 <pid>
```

You can also terminate processes by name:

```
pkill firefox
```

## 8. niceness

Niceness is a value affecting process priority; lower niceness means higher priority. You would want critical system infrastructure to have a lower value. You can start a process with a niceness (priority) value:

```
nice -n 10 command
```

Change an existing process’s niceness:

```
renice 5 <pid>
```

## 9. Process States

Processes are in states such as:

- Running (R)
- Sleeping (S)
- Stopped (T)
- **I**: Idle kernel thread (a kernel thread that is currently idle)
- Zombie (Z) — a terminated process waiting for parent cleanup

View states in `ps`:

```
ps -eo pid,state,cmd
```

## 10. /proc Filesystem

`/proc` is a virtual filesystem exposing detailed info about processes and system status. Each process has a directory `/proc/<pid>` with files describing it. View proc systems with:

```
ls /proc
```

Explore /proc for CPU info, memory usage, open files, and more.

```
cat /proc/<pid>/status
```

## 11. Job Control

Job control allows managing background and foreground processes interactively in shells. Important commands:

- `bg` — resume job in background
- `fg` — bring job to foreground
- `jobs` — list current jobs

### Job Control Example:

Step 1: Start a long-running job in the background

```
sleep 300 &
```

Output will look like: 

> [1] 12345 (job number and process ID)

Step 2: List the jobs

```
jobs
```

Output example:

> [1]+ Running sleep 300 &


Step 3: Stop a foreground job (start one first)

```
sleep 500
```

Press CTRL+Z to pause it

You'll see:

> [2]+ Stopped sleep 500

Step 4: Resume it in the background

```
bg %2
```

Output: 

> [2]+ sleep 500 &

Step 5: Bring it back to the foreground

```
fg %2
```

Now you are attached to it again

To kill a job you can do

```
kill %<job number>
```

## Follow Us on Social Media

[YouTube](https://www.youtube.com/@learntohomelab)

[Discord](https://discord.gg/6MsHSJWZpH)

[Patreon](https://www.patreon.com/c/learntohomelab)

[Reddit](https://www.reddit.com/r/learntohomelab/)

[Rumble](https://rumble.com/c/c-7585051)