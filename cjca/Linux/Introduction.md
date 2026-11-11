
# Linux Structure

### 1. Linux Overview

- Linux: Open-source operating system kernel used in servers, desktops, embedded systems, and Android.
- Operating System (OS): Manages hardware resources and communication between hardware and software.
- Distribution (Distro): A Linux-based OS that includes the kernel, software, and utilities. Examples: Ubuntu, Debian, Fedora, Kali, Parrot.
- Parrot OS: Debian-based distribution focused on security, privacy, and development.

### 2. Linux History

- 1970: Unix released by Ken Thompson and Dennis Ritchie.
- 1977: BSD released.
- 1983: Richard Stallman started the GNU Project.
- 1991: Linus Torvalds created the Linux kernel.
- GNU GPL v2: License used by the Linux kernel.

### 3. Linux Philosophy

- Everything is a File: System resources are represented through file-like interfaces.
- Small Programs: Each program performs one specific task.
- Chaining Programs: Combine commands using pipes (`|`) to perform complex tasks.
- Shell Interaction: Control the system through the terminal.
- Text-based Configuration: Configuration is stored in text files, such as `/etc/passwd`.

### 4. Linux Components

- Bootloader: Starts the boot process and loads the OS (GRUB).
- Kernel: Manages hardware resources and system operations.
- Daemons: Background services responsible for system functions.
- Shell: Command interpreter between the user and OS (Bash, Zsh, Fish).
- Graphics Server: Provides graphical display services (X Server).
- Window Manager: Manages graphical windows and desktop environments (GNOME, KDE, MATE).
- Utilities: Programs that perform specific tasks.

### 5. Linux Architecture

Linux consists of four main layers:

1. Hardware: CPU, RAM, HDD, and peripheral devices.
2. Kernel: Controls hardware resources, memory, and processes.
3. Shell: Command-line interface (CLI) used to execute commands.
4. System Utilities: Tools that provide operating system functionality.

### 6. Linux Filesystem Hierarchy (FHS)

Linux uses a tree-like filesystem structure starting from the root directory `/`.

- `/` : Root directory; top of the filesystem.
- `/bin` : Essential command binaries.
- `/boot` : Kernel and bootloader files.
- `/dev` : Device files.
- `/etc` : System configuration files.
- `/home` : Regular users' home directories.
- `/lib` : Essential shared libraries.
- `/media` : Removable devices (USB, CD).
- `/mnt` : Temporary mount point.
- `/opt` : Optional and third-party software.
- `/root` : Root user's home directory.
- `/sbin` : System administration binaries.
- `/tmp` : Temporary files.
- `/usr` : Applications, libraries, and documentation.
- `/var` : Variable data, logs, mail, and web-related files.


