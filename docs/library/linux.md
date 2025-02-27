# 

## Linux 100

<div class="grid" markdown>

??? abstract "Navigation & Basics Commands"
    ??? question "man"
    ??? question "cd"
    ??? question "pwd"
    ??? question "ls"
    ??? question "tree"
    ??? abstract "Moving Files/Dirs"
        ??? question "mv"
            ```bash
            mv [option] source destination
            ```
    ??? abstract "Creating Files/Dirs"
        ??? question "touch"
            ```bash
            touch newfile.txt
            ```
        ??? question "cat"
            ```bash
            cat > newfile.txt
            ```
        ??? question "echo"
            ```bash
            echo "hello world!" > newfile.txt
            ```
        ??? question "mkdir"
    ??? abstract "Deleting Files/Dirs"
        ??? warning "rm"
            ```bash
            rm unwantedfile.txt
            rm -i unwantedfile.txt # (1)!
            ```

            1. :man_raising_hand: `rm -i` (interactive) to ask for confirmation before deleting.
        ??? warning "rmdir"
            `rm [empty dir]`
    ??? abstract "Filesystem Hierarchy Standard (FHS)"
        ??? question "/"
            Root dir, the top level of the file system
        ??? question "/home"
            User home dirs
        ??? question "/bin"
            Essential binary executables
        ??? question "/sbin"
            System administration binaries
        ??? question "/etc"
            Configuration files
        ??? question "/var"
            Variable data (logs, spool files)
        ??? question "/usr"
            User programs and data
        ??? question "/lib"
            Shared libraries
        ??? question "/tmp"
            Temporary files
??? abstract "Editing Files"
    ??? question "vim"
        ```bash
        vim example.txt
        ```
        To insert new content, press `i` for 'insert mode'. After editing, press `ESC` to go back to 'command mode', and type `:wq` to save and quit.
    ??? question "nano"
        ```bash
        nano exmaple.txt
        ```
        Installation for Ubuntu based distributions
        ``` bash
        sudo apt update
        sudo apt installl nano
        ```
        Installation for Arch Linux
        ```bash
        sudo pacman -S nano
        ```
??? abstract "Linux Shell Basics"
    ??? question "Command Path in Shell"
        In Linux, the command path is an important concept under shell basics. Simply put, command path is a variable that is used by the shell to determine where to look for the executable files to run. Linux commands are nothing but programs residing in particular directories. But, one does not have to navigate to these directories every time to run these programs. The command path comes to the rescue!

        Usually, when you type a command in the terminal, the shell needs to know the absolute path of the command's executable to run it. Instead of typing the full path each time, command paths allow the shell to automatically search the indicated directories in the correct order. These paths are stored in the $PATH environment variable.
        ```bash
        echo $PATH
        ```
        !!! tip "[Mini-Project] What happen when you type a Linux command?"
    ??? question "Environment Variables under Shell"
        List all the environment Variables
        ```bash
        env
        ```
        !!! info "Remember, every shell, such as Bourne shell, C shell, or Korn shell in Unix or Linux has different syntax and semantics to define and use environment variables."
    ??? question "Command Help"
        To view the manual entry for any command
        ```bash
        man [command]
        ```
        For built-in shell functions
        ```bash
        help [command]
        ```
        To view examples with TLDR
        ```bash
        tldr [command]
        ```
    ??? question "Redirects in Shell"
        The shell in Linux provides a robust way of managing input and output streams of a command or program, this mechanism is known as Redirection. Linux being a multi-user and multi-tasking operating system, every process typically has 3 streams opened:

        * Standard Input (stdin) - This is where the process reads its input from. The default is the keyboard.
        * Standard Output (stdout) - The process writes its output to stdout. By default, this means the terminal.
        * Standard Error (stderr) - The process writes error messages to stderr. This also goes to the terminal by default.
        
        Redirection in Linux allows us to manipulate these streams, advancing the flexibility with which commands or programs are run. Besides the default devices (keyboard for input and terminal for output), the I/O streams can be redirected to files or other devices.

        !!! example "If you want to store the output of a command into a file instead of printing it to the console, we can use the `>` operator."
            ```bash
            ls -al > file_list.txt
            ```
            This command will write the output of `ls -al` into `file_list.txt`, whether or not the file initially existed. It will be created if necessary, and if it already exists - it will be overwritten.
    ??? question "Super User"
        The Super User, also known as “root user”, represents a user account in Linux with extensive powers, privileges, and capabilities. This user has complete control over the system and can access any data stored on it. This includes the ability to modify system configurations, change other user’s passwords, install software, and perform more administrative tasks in the shell environment.
        
        Switches the current user to the root
        ```bash
        su -
        ```
        Allows you to run a command as another user, default being root
        ```bash
        sudo [commmand]
        ```
        !!! danger "Super User privileges should be handled with care due to their potential to disrupt the system’s functionality. Mistaken changes to key system files or unauthorized access can lead to severe issues."
??? abstract "Working with Files"
    In Linux, everything is considered a file: texts, images, systems, devices, and directories.
    ??? question "Linux File Permissions"
        ??? example "-rwxr--r-- 1 root root 4096 Jan 1 12:00 filename"

            * The first character: `-` for a file, `d` for a dir.
            * The first group of three characters: represents the permissions for the owner. (`rwx`)
            * The next group of three characters: represents the permissions for the group. (`r--`)
            * The last group of three characters: represents the permission for the others. (`r--`)

            The `r` indicates that the file can be read, `w` indicates that the file can be written to, and `x` indicates that the file can be executed.

        ??? question "chmod"
        ??? question "chown"
        ??? question "chgrp"
    ??? question "Archiving & Compression"
        In Linux, archiving and compression are separate processes, hence tar to archive and gzip/bzip2 to compress. Although they’re commonly used together, they can very much be used separately as per the requirements.
        
        Create a tar archive
        ```bash
        tar cvf archive_name.tar dir_to_archive/
        ```
        Extract a tar archive
        ```bash
        tar xvf archive_name.tar
        ```
        Create a gzip compressed tar archive
        ```bash
        tar cvzf archive_name.tar.gz dir_to_archive/
        ```
        Create a bzip2 compressed tar archive
        ```bash
        tar cvjf archive_name.tar.bz2 dir_to_archive/
        ```
    ??? question "Copying & Renaming Files"
        To copy files
        ```bash
        cp /path/to/original/file /path/to/copied/file
        ```
        To rename files
        ```bash
        mv /path/to/original/file /path/to/new/file
        ```
    ??? question "Soft & Hard Links"
        A hard link is a mirror reflection of the original file, sharing the same file data and inode number, but displaying a different name. It’s vital to note that if the original file is deleted, the hard link still retains the file data.
        ```bash
        ln source_file.txt hard_link.txt
        ```
        A soft link, also known as a symbolic link, is more like a shortcut to the original file. It has a different inode number and the file data resides only in the original file. If the original file is removed, the symbolic link breaks and will not work until the original file is restored.
        ```bash
        ln -s source_file.txt soft_link.txt
        ```
??? abstract "Text Processing"
    ??? question "awk"
        `awk` is adept at performing operations upon text files, such as sorting, filtering, and report generation.
        
        The language comprises a set of commands within a script that define pattern-action pairs. Essentially, awk reads an input file line by line, identifies patterns that match what is specified in the script, and consequently executes actions upon those matches.
        ```bash
        awk '{pattern-action pairs}' [filename]
        ```
        !!! example "awk {print \$1,\$2}' file.txt"
            ```bash title="cat file.txt"
            file.txt file2.txt file3.txt
            dir.txt dir2.txt dir3.txt
            drive.txt drive2.txt drive3.txt
            port.txt port2.txt port3.txt
            ```
            ```bash title="awk '{print $1,$2}' file.txt"
            file.txt file2.txt
            dir.txt dir2.txt
            drive.txt drive2.txt
            port.txt port2.txt
            ```
            This would display the first and second field (typically separated by spaces) of every line in `file.txt`.
    ??? question "grep"
        GREP (Global Regular Expression Print) is considered a significant tool in text processing area on Unix-like operating systems including Linux. It is a powerful utility that searches and filters text matching a given pattern. When it identifies a line that matches the pattern, it prints the line to the screen, offering an effective and a codified way to find text within files.
        ```bash
        grep "pattern" [filename]
        ```
        !!! example "grep 'e.txt' file.txt"
            ```bash title="cat file.txt"
            file.txt
            dir.txt
            drive.txt
            port.txt
            ```
            ```bash title="grep 'e.txt' file.txt"
            file.txt
            drive.txt
            ```
            This command will search for the specified pattern within the file and prints the line to the terminal.
    ??? question "ripgrep"
        There is also an alternative to `grep` - `ripgrep`.

        `ripgrep` is an extremely fast text processor that supports all the features of `grep` and extends it.
    ??? question "uniq"
        In Linux, uniq is an extremely useful command-line program for text processing. It aids in the examination and manipulation of text files by comparing or filtering out repeated lines that are adjacent. Whether you’re dealing with a list of data or a large text document, the uniq command allows you to find and filter out duplicate lines, or even provide a count of each unique line in a file. It’s important to remember that uniq only removes duplicates that are next to each other, so to get the most out of this command, data is often sorted using the sort command first.
        ```bash
        sort [filename] | uniq
        ```
        !!! example "sort names.txt | uniq"
            `names.txt` is a file containing a list of names. The `sort` command sorts all the lines in the file, and then the `uniq` command removes all the duplicate lines. The resulting output would be a list of unique names from `names.txt`.
    ??? question "unexpand"
        This command works by replacing spaces with tabs, making a document or output more coherent and neat.

        It is primarily used to format the structure, particularly in programming scripts, where indenting with tabs is a common practice.
        ```bash
        unexpand [options] [filename]
        ```
        !!! example "unexpand -t 4 file.txt"
            The `-t 4` switch tells `unexpand` to replace every four spaces in `file.txt` with a tab.
    ??? question "expand"
        It can be an essential tool while working with file outputs where the formatting can get disturbed due to tabs. This can be especially useful when working with Linux shell scripts, where the tab space might differ on different systems or text editors, resulting in inconsistent formatting. Consistent indentation using space can greatly enhance code readability.
        ```bash
        expand [options] [filename]
        ```
        !!! example "expand file.txt"
            The `expand` command by default converts tabs into 8 spaces.
        !!! example "expand -t 4 file.txt"
            Each tab character in file.txt will be replaced with 4 spaces. The output would then be displayed on the console.
    ??? question "wc"
        The `wc` command is a commonly used tool in Unix or Linux that allows users to count the number of bytes, characters, words, and lines in a file or in data piped from standard input. The name `wc` stands for ‘word count’, but it can do much more than just count words. Common usage of `wc` includes tracking program output, counting code lines, and more. It’s an invaluable tool for analyzing text at both granular and larger scales
        ```bash
        wc [options] [filename]
        ```
        !!! example "wc file.txt"
            ```bash title="cat file.txt"
            file.txt
            dir.txt
            drive.txt
            port.txt
            ```
            ```bash title="wc file.txt"
            3  4 35 file.txt
            ```
            This command would output the number of lines, words, and characters in `file.txt`. The output is displayed in the following order: line count, word count, character count, followed by the filename.
    ??? question "nl"
        `nl` command in Linux is a utility for numbering lines in a text file. Also known as ‘number lines’, it can be handy when you need an overview where certain lines in a file are located. By default, nl number the non-empty lines only, but this behavior can be modified based on user’s needs.
        ```bash
        nl [options] [filename]
        ```
        !!! example "nl file.txt"
            ```bash title="cat file.txt"
            file.txt
            dir.txt
            drive.txt
            port.txt
            ```
            ```bash title="nl file.txt"
                1  file.txt
                2  dir.txt
                3  drive.txt
                4  port.txt
            ```
            If no file is specified, `nl` will wait for input from user’s terminal (stdin). Its clear and readable output makes it a valuable part of any Linux user’s text processing toolkit.
    ??? question "tee"
        `tee` command reads from the standard input and writes to standard output and files. This operation gets its name from the T-splitter in plumbing, which splits the flow into two directions, paralleling the function of the tee command.
        ```bash
        [command] | tee file
        ```
        !!! example "ls | tee file.txt"
            ```bash title="ls | tee file.txt"
            file.txt
            ```
            ```bash title="cat file.txt"
            file.txt
            ```
            `ls` lists the files in the current directory from which `tee` reads the output, and `file.txt` signifies the file where `tee` writes the output.
    ??? question "|"
        The pipe (`|`) is a powerful feature in Linux used to connect two or more commands together. This mechanism allows output of one command to be “piped” as input to another.
        ```bash
        [command 1] | [command 2] | ...
        ```
        !!! example "ls | grep '\.txt$'"
            `ls` lists the files in the current directory and grep `\.txt$` filters out any files that don’t end with `.txt`. The pipe command, `|`, takes the output from `ls` and uses it as the input to grep `\.txt$`. The output of the entire command is the list of text files in the current directory.
    ??? question "split"
        The `split` command in Linux divides a file into multiple equal parts, based on the lines or bytes specified by the user.
        ```bash
        split [options] [input [prefix]]
        ```
        !!! example "split bigfile.txt"
            By default, the `split` command divides the file into smaller files of 1000 lines each. If no input file is provided, or if it is given as `-`, it reads from standard input.
        !!! example "split -l 500 bigfile.txt"
            Split a file named `bigfile.txt `into files of 500 lines each.
    ??? question "join"
        `join` to combine lines of two files on a common field.
        ```bash
        join [filename_first] [filename_second]
        ```
        !!! example "join file1.txt file2.txt"
            ```bash title="cat file1.txt"
            item1 10
            item2 20
            ```
            ```bash title="cat file2.txt"
            item1 10$
            item2 20$
            ```
            ```bash title="join file1.txt file2.txt"
            item1 10 10$
            item2 20 20$
            ```
            If you have two files that have a list of items, one with costs and the other with quantities, you can use join to combine these two files so each item has a cost and quantity on the same line.
    ??? question "tail"
        The `tail` command reads data from standard input or from a file and outputs the last `N` bytes, lines, blocks, characters or words to the standard output (or a different file).
        ```bash
        tail [options] [filename]
        ```
        !!! example "tail /var/log/syslog"
            By default, the `tail` command will print the last 10 lines of the `/var/log/syslog` file.
    ??? question "head"
        The `tail` command reads data from standard input or from a file and outputs the first `N` bytes, lines, blocks, characters or words to the standard output (or a different file).
        ```bash
        head [options] [filename]
        ```
        !!! example "head /var/log/syslog"
            By default, the `head` command will print the first 10 lines of the `/var/log/syslog` file.
        !!! example "head -n 5 /var/log/syslog"
            Print the first 5 lines of the `/var/log/syslog` file.
    ??? question "tr"
        The `tr` command in Linux is a command-line utility that translates or substitutes characters. It reads from the standard input and writes to the standard output. Although commonly used for translation applications, `tr` has versatile functionality in the text processing aspect of Linux. Ranging from replacing a list of characters, to deleting or squeezing character repetitions, `tr` presents a robust tool for stream-based text manipulations.
        ```bash
        [command] | tr [pattern] [new_pattern]
        ```
        !!! example "cat file.txt | tr 'a-z' 'A-Z'"
            ```bash title="cat file.txt"
            file.txt file2.txt file3.txt
            dir.txt dir2.txt dir3.txt
            drive.txt drive2.txt drive3.txt
            port.txt port2.txt port3.txt
            ```
            ```bash title="cat file.txt | tr 'a-z' 'A-Z'"
            FILE.TXT FILE2.TXT FILE3.TXT
            DIR.TXT DIR2.TXT DIR3.TXT
            DRIVE.TXT DRIVE2.TXT DRIVE3.TXT
            PORT.TXT PORT2.TXT PORT3.TXT
            ```
            `tr` is used to convert the lowercase in the `file.txt` to uppercase.
    ??? question "sort"
        The `sort` command in Linux is used to sort the contents of a text file, line by line. The command uses ASCII values to sort files. You can use this command to sort the data in a file in a number of different ways such as alphabetically, numerically, reverse order, or even monthly. The sort command takes a file as input and prints the sorted content on the standard output (screen).
        ```bash
        sort [options] [filename]
        ```
        !!! example "sort file.txt"
            ```bash title="cat file.txt"
                file.txt file2.txt file3.txt
                dir.txt dir2.txt dir3.txt
                drive.txt drive2.txt drive3.txt
                port.txt port2.txt port3.txt
            ```
            ```bash title="sort file.txt"
                dir.txt dir2.txt dir3.txt
                drive.txt drive2.txt drive3.txt
                file.txt file2.txt file3.txt
                port.txt port2.txt port3.txt
            ```
            This command prints the sorted content of the filename.txt file. The original file content remains unchanged.
        !!! example "sort file.txt > sorted_file.txt"
            ```bash title="cat file.txt"
                file.txt file2.txt file3.txt
                dir.txt dir2.txt dir3.txt
                drive.txt drive2.txt drive3.txt
                port.txt port2.txt port3.txt
            ```
            ```bash title="sort file.txt > sorted_file.txt"
            ```
            ```bash title="cat file.txt"
                file.txt file2.txt file3.txt
                dir.txt dir2.txt dir3.txt
                drive.txt drive2.txt drive3.txt
                port.txt port2.txt port3.txt
            ```
            ```bash title="cat sorted_file.txt"
                dir.txt dir2.txt dir3.txt
                drive.txt drive2.txt drive3.txt
                file.txt file2.txt file3.txt
                port.txt port2.txt port3.txt
            ```
    ??? question "paste"
        `paste` is a powerful text processing utility that is primarily used for merging lines from multiple files. It allows users to combine data by columns rather than rows, adding immense flexibility to textual data manipulation. Users can choose a specific delimiter for separating columns, providing a range of ways to format the output.
        ```bash
        paste [filename_first] [filename_second]
        ```
        !!! example "paste file1.txt file2.txt"
            ```bash title="cat file1.txt"
            item1 10
            item2 20
            ```
            ```bash title="cat file2.txt"
            item1 10$
            item2 20$
            ```
            ```bash title="paste file1.txt file2.txt"
            item1 10        item1 10$
            item2 20        item2 20$
            ```
    ??? question "cut"
        The `cut` command is a text processing utility that allows you to cut out sections of each line from a file or output, and display it on the standard output (usually, the terminal). It’s commonly used in scripts and pipelines, especially for file operations and text manipulation.

        This command is extremely helpful when you only need certain parts of the file, such as a column, a range of columns, or a specific field. For example, with Linux system logs or CSV files, you might only be interested in certain bits of information.
        ```bash
        cut OPTION... [FILE]...
        ```
        !!! example "echo "one,two,three,four" | cut -d "," -f 2"
            This command will output the second field (`two`) by using the comma as a field delimiter (`-d ","`).
    ??? question "stdout / stdin / stderr"
        The concepts of stdout and stderr in Linux belong to the fundamentals of Linux text processing. In Linux, when a program is executed, three communication channels are typically opened, namely, STDIN (Standard Input), STDOUT (Standard Output), and STDERR (Standard Error).

        Each of these channels has a specific function. STDOUT is the channel through which the output from most shell commands is sent. STDERR, on the other hand, is used specifically for sending error messages. This distinction is very useful when scripting or programming, as it allows you to handle normal output and error messages in different manners.
        ```bash
        [command] > stdout.txt 2> stderr.txt
        ```
        !!! example "ls > stdout.txt 2> stderr.txt"
            ```bash title="cat stdout.txt"
                file1.txt
                file2.txt
                file.txt
                sorted_file.txt
                stderr.txt
                stdout.txt
            ```
            ```bash title="cat stderr.txt"
            ```
        !!! example "ls bad-options-blablabla > stdout.txt 2> stderr.txt"
            ```bash title="cat stdout.txt"
            ```
            ```bash title="cat stderr.txt"
            ls: cannot access 'bad-options-blablabla': No such file or directory
            ```
??? abstract "Server Review"
    ??? question "Uptime Load"
        When managing a Linux server, one critical metric deserving close scrutiny is the “uptime”. The `uptime` command in Linux gives information about how long the system has been running without shutting down or restarting, and the system load average.

        The system load average is an important indicator that illustrates the amount of computational work that a computer system performs. It’s a reflection of how many processes are waiting in line to get CPU time. The system load average is typically shown for 1, 5, and 15 minutes durations.

        By consistently analyzing the uptime and load on a Linux server, administrators can identify system usage patterns, diagnose possible performance issues, and determine an efficient capacity planning strategy. If a server has a high load average, it may suggest that the system resources are not sufficient or are misconfigured, leading to possible slow performance or system unresponsiveness.
        !!! example "Uptime and Load"
            ```bash title="uptime"
             10:58:35 up 2 days, 20 min,  1 user,  load average: 0.00, 0.01, 0.05
            ```
            “2 days, 20 min” tells us how long the system has been up, while “0.00, 0.01, 0.05” shows the system’s load average over the last one, five, and fifteen minutes, respectively.
    ??? question "Authentication Logs"
        When dealing with a Linux server and its maintenance, one of the most critical components to regularly review is the auth logs. These logs, usually located in `/var/log/auth.log` (for Debian-based distributions) or `/var/log/secure` (for Red Hat and CentOS), record all authentication-related events and activities which have occurred on the server. This includes, among others, system logins, password changes, and issued sudo commands.

        Auth logs are an invaluable tool for monitoring and analyzing the security of your Linux server. They can indicate brute force login attacks, unauthorized access attempts, and any suspicious behavior. Regular analysis of these logs is a fundamental task in ensuring server security and data integrity.
        !!! example "View authentication log"
            ```bash title="tail /var/log/auth.log"
            Feb 21 09:28:18 server-prod su: (to root) debian on pts/0
            Feb 21 09:28:18 server-prod su: pam_unix(su:session): session opened for user root by debian(uid=0)
            Feb 21 09:28:18 server-prod sshd[6346]: pam_unix(sshd:auth): authentication failure; logname= uid=0 euid=0 tty=ssh ruser= rhost=18.9.14.18  user=root
            Feb 21 09:28:20 server-prod sshd[6346]: Failed password for root from 18.9.14.18 port 37752 ssh2
            Feb 21 09:28:21 server-prod sshd[6346]: Connection closed by authenticating user root 18.9.14.18 port 37752 [preauth]
            Feb 21 09:28:26 server-prod sshd[6368]: Invalid user bigdata from 18.9.14.18 port 54708
            Feb 21 09:28:27 server-prod sshd[6368]: pam_unix(sshd:auth): check pass; user unknown
            Feb 21 09:28:27 server-prod sshd[6368]: pam_unix(sshd:auth): authentication failure; logname= uid=0 euid=0 tty=ssh ruser= rhost=18.9.14.18 
            Feb 21 09:28:28 server-prod sshd[6368]: Failed password for invalid user bigdata from 18.9.14.18 port 54708 ssh2
            Feb 21 09:28:30 server-prod sshd[6368]: Connection closed by invalid user bigdata 18.9.14.18 port 54708 [preauth]
            ```
    ??? question "Services Running"
        Linux servers are popular for their stability and flexibility, factors that make them a preferred choice for businesses and organizations when it comes to managing various services. Services that run under a Linux server can range from web services to database services, DNS servers, mail servers, and many others.

        As a Linux system administrator, it’s important to periodically review these running services to manage resources, check their statuses, and troubleshoot issues, ensuring the health and performance of the server.

        Linux has a variety of tools to achieve this, such as: `systemctl`, `service`, `netstat`, `ss` and `lsof`.
        !!! example "systemctl --type=service"
            ```bash title="systemctl --type=service"
                UNIT               LOAD   ACTIVE SUB     DESCRIPTION                                     
                apparmor.service   loaded active exited  Load AppArmor profiles
                cron.service       loaded active running Regular background program processing daemon
                ...                ...    ...    ...     ... 
                unscd.service      loaded active running Name Service Cache  Daemon 
                user@1000.service  loaded active running User Manager for UID 1000

                LOAD   = Reflects whether the unit definition was properly loaded.
                ACTIVE = The high-level unit activation state, i.e. generalization of SUB.
                SUB    = The low-level unit activation state, values depend on unit type.

                47 loaded units listed. Pass --all to see loaded but inactive units, too.
                To show all installed unit files use 'systemctl list-unit-files'.
            ```
    ??? question "Available Memory/Disk"
        ??? question "free"
            Gives a summary of the overall memory usage including total used and free memory, swap memory and buffer/cache memory.
            !!! example "free -h"
            ```bash title="free -h"
                            total       used        free      shared  buff/cache   available
                Mem:         14Gi      519Mi        11Gi       274Mi       2.4Gi        13Gi
                Swap:          0B         0B          0B
            ```
            the `-h` option is used to present the results in a human-readable format
        ??? question "vmstat"
        ??? question "top" 
??? abstract "Process Management"
    ??? question "Background / Foreground Processes"
        In Linux environment, a process can be run in either the foreground (fg) or the background (bg). The foreground process takes input directly from the user, displaying output and errors to the user’s terminal. On the other hand, a background process runs independently of the user’s actions, freeing up the terminal for other tasks.

        Typically, a process starts in the foreground. However, you can send it to the background by appending an ampersand (`&`) to the command or by using the `bg` command. Conversely, the `fg` command brings a background process to the foreground.
        ```bash title="send a running process to background"
        [command] &
        ```
        ```bash title="if a process is already running"
        CTRL + Z # (1)!
        bg # (2)!
        ```

        1. This will pause the process
        2. This resumes the paused process in the background
        
        ```bash title="bring it back to the foreground"
        fg
        ```
        These commands, `bg` and `fg` are part of job control in Unix-like operating systems, which lets you manage multiple tasks simultaneously from a single terminal
    ??? question "Listing / Finding Processes"
        The proc filesystem is an extremely powerful tool in this respect. Available in all Unix-like operating systems, proc is a virtual file system that provides detailed information about running processes, including its PID, status, and resource consumption.

        With commands like ps, top, and htop, we can quickly list out the running processes on the Linux system. Specifically, the ps command offers an in-depth snapshot of currently running processes, whereas top and htop give real-time views of system performance.
        !!! question "ps -ef"
            List all runningj processes.
        !!! question "top"
            Display ongoing list of running processes.
        !!! question "htop"
            `top` alternatively, for a more user-friendly interface.
        Exploring the proc directory (/proc), we dive even deeper, enabling us to view the system’s kernel parameters and each process’s specific system details.
        !!! question "cat /proc/{PID}/status"
            View specifics of a particular PID
    ??? question "Process Signals"
        Process signals are a form of communication mechanism in Unix and Linux systems. They provide a means to notify a process of synchronous or asynchronous events. There are a variety of signals like SIGINT, SIGSTOP, SIGKILL, etc. available which can be sent to a running process to interrupt, pause or terminate it.
        !!! example "kill -SIGSTOP {PID}"
            Send a SIGSTOP signal to a process with a PID. This will suspend the execution of the process until a SIGCONT signal is received.
    ??? question "Process Priorities"
        In the Linux environment, every running task or essentially a “process” is assigned a certain priority level that impacts its execution timing. These priorities are instrumental in efficient system resource utilization, enabling Linux to fine-tune execution and allocate system resources smartly.

        The Linux kernel sorts processes in the proc structure, typically found under the `/proc` file system directory. This structure contains information about all active processes, including their priorities. The concept of proc priorities under process management refers to the priority accorded to each process by the system. This priority value (also known as “nice” value) ranges from -20 (highest priority) to +19 (lowest priority).

        By understanding and managing proc priorities, you can optimize system performance and control which processes receive more or less of the CPU’s attention.
        !!! example "View all PIDs with Priorities and Users"
            Display the process ID, priority, and user for all processes.
            ```bash title="ps -eo pid,pri,user"
            PID   PRI USER
            1     19  root
            2     19  root
            ...   ... ...
            4488  19  chanvi
            ```
        !!! example "Change priority of a PID"
            ```bash
            renice [nice_value] [option] [PID]
            ```
            !!! example "Increase priority by 5 units for process ID 4488"
                ```bash title="ps -eo pid,pri,user"
                PID   PRI USER
                1     19  root
                2     19  root
                ...   ... ...
                4488  19  chanvi
                ```
                ```bash title="renice -5 -p 4488"
                4488 (process ID) old priority 0, new priority -5
                ```
                ```bash title="ps -eo pid,pri,user"
                PID   PRI USER
                1     19  root
                2     19  root
                ...   ... ...
                4488  24  chanvi
                ```
    ??? question "Killing Processes"
        On any Linux system, whether you’re on a server or a desktop system, processes are consistently running. Sometimes, these processes may not behave as expected due to certain reasons like system bugs, unexpected system behavior, or accidental initiation and may require termination. This is where the concept of killing processes in Linux comes to picture under the area of process management.

        `kill` in Linux is a built-in command that is used to terminate processes manually. You can use the `kill` command to send a specific signal to a process. When we use the `kill` command, we basically request a process to stop, pause, or terminate
        ```bash
        kill [signal or option] PID(s)
        ```
        > In practice, you would identify the Process ID (PID) of the process you want to terminate and replace PID(s) in the above command. The signal or option part is optional, but very powerful allowing for specific termination actions.
    ??? question "Process Forking"
        Process forking is a fundamental concept under process management in Linux systems. The term refers to the mechanism where a running process (parent process) can generate a copy of itself (child process), enabling concurrent execution of both processes. This is facilitated by the ‘fork’ system call. It is a prominent aspect in understanding the creation and control of processes in a Linux environment.

        The child process created by fork is a nearly perfect copy of the parent process with exception to just a few values including the process ID and parent process ID. Any changes made in the child process does not affect the parent process, and vice versa.

        ```C title="Basic code snippet of proc forking in C"
        #include<sys/types.h>
        #include<unistd.h>
        #include<stdio.h>

        int main()
        {
            pid_t child_pid;

            // Try creating a child process
            child_pid = fork();

            // If a child is successfully created
            if(child_pid >= 0)
            printf("Child created with PID: %d\n", child_pid);
            else
            printf("Fork failed\n");
            return 0;
        }
        ```
        > In this snippet, `fork()` is used to created a new child process. If the process creation is successful, `fork()` returns the process ID of the child process. If unsuccessful, it returns a negative value.
??? abstract "User Management"
    ??? question "Create/Delete/Update Users"
        ```bash title="Create new users"
        useradd [username] # (1)!
        ```
        
        1. Alternative, `adduser [username]`

        ```bash title="Update user's details (home dir or login shell)"
        usermod
        ```
        ```bash title="Delete users"
        userdel [username]
        ```
    ??? question "Users and Groups"
        User management in Linux uses user groups to manage system users and permissions efficiently. A user group is a collection of users that simplifies system administration by determining access rights to resources like files and directories. Each user belongs to one or more groups, allowing administrators to grant specific privileges without full superuser access. 
        ```bash title="groupadd"
        groupadd
        ```
        ```bash title="groupmod"
        groupmod
        ```
        ```bash title="groupdel"
        groupdel
        ```        
        ```bash title="usermod"
        usermod
        ```    
        ```bash title="gpasswd"
        gpasswd
        ```    
    ??? question "Managing Permissions"
        User management in Linux involves managing permissions to control who can access, modify, and execute files and directories. Permissions are categorized into read, write, and execute types and can be set for the file owner (user), the owning group, and others.
        ```bash title="chmod"
        chmod
        ```        
        ```bash title="chown"
        chown
        ```    
        ```bash title="chgrp"
        chgrp
        ```    
??? abstract "Service Management(systemd)"
    ??? question "Checking Service Status"
        ```bash
        systemctl status [service_name]
        ```
        !!! example "Check PostgreSQL status"
            ```bash title="systemctl status postgresql"
            ● postgresql.service - PostgreSQL RDBMS
                Loaded: loaded (/usr/lib/systemd/system/postgresql.service; enabled; preset: enabled)
                Active: active (exited) since Tue 2025-02-25 08:49:01 +07; 2h 57min ago
            Main PID: 2535 (code=exited, status=0/SUCCESS)
                    CPU: 726us

            Feb 25 08:49:01 chanvi-Dell-G15-5520 systemd[1]: Starting postgresql.service - PostgreSQL RDBMS...
            Feb 25 08:49:01 chanvi-Dell-G15-5520 systemd[1]: Finished postgresql.service - PostgreSQL RDBMS.
            ```
    ??? question "Start/Stop Services"
        ```bash
        systemctl [stop|start|restart] [service_name]
        ```
        !!! example "Stop a service"
            ```bash title="systemctl stop postgresql"
            ```
            ```bash title="systemctl status postgresql"
            ○ postgresql.service - PostgreSQL RDBMS
                Loaded: loaded (/usr/lib/systemd/system/postgresql.service; enabled; preset: enabled)
                Active: inactive (dead) since Tue 2025-02-25 14:23:09 +07; 5s ago
            Duration: 16.311s
                Process: 59550 ExecStart=/bin/true (code=exited, status=0/SUCCESS)
            Main PID: 59550 (code=exited, status=0/SUCCESS)
                    CPU: 2ms

            Feb 25 14:22:53 chanvi-Dell-G15-5520 systemd[1]: Starting postgresql.service - PostgreSQL RDBMS...
            Feb 25 14:22:53 chanvi-Dell-G15-5520 systemd[1]: Finished postgresql.service - PostgreSQL RDBMS.
            Feb 25 14:23:09 chanvi-Dell-G15-5520 systemd[1]: postgresql.service: Deactivated successfully.
            Feb 25 14:23:09 chanvi-Dell-G15-5520 systemd[1]: Stopped postgresql.service - PostgreSQL RDBMS.
            ```
        !!! example "Start a service"
            ```bash title="systemctl start postgresql"
            ```
            ```bash title="systemctl status postgresql"
            ● postgresql.service - PostgreSQL RDBMS
                Loaded: loaded (/usr/lib/systemd/system/postgresql.service; enabled; preset: enabled)
                Active: active (exited) since Tue 2025-02-25 14:25:53 +07; 2s ago
                Process: 60645 ExecStart=/bin/true (code=exited, status=0/SUCCESS)
            Main PID: 60645 (code=exited, status=0/SUCCESS)
                    CPU: 1ms

            Feb 25 14:25:53 chanvi-Dell-G15-5520 systemd[1]: Starting postgresql.service - PostgreSQL RDBMS...
            Feb 25 14:25:53 chanvi-Dell-G15-5520 systemd[1]: Finished postgresql.service - PostgreSQL RDBMS.
            ```
        !!! example "Restart a service"
            ```bash title="systemctl restart postgresql"
            ```
            ```bash title="systemctl status postgresql"
            ● postgresql.service - PostgreSQL RDBMS
                Loaded: loaded (/usr/lib/systemd/system/postgresql.service; enabled; preset: enabled)
                Active: active (exited) since Tue 2025-02-25 14:29:02 +07; 3s ago
                Process: 63540 ExecStart=/bin/true (code=exited, status=0/SUCCESS)
            Main PID: 63540 (code=exited, status=0/SUCCESS)
                    CPU: 2ms

            Feb 25 14:29:02 chanvi-Dell-G15-5520 systemd[1]: Starting postgresql.service - PostgreSQL RDBMS...
            Feb 25 14:29:02 chanvi-Dell-G15-5520 systemd[1]: Finished postgresql.service - PostgreSQL RDBMS.
            ```   
    ??? question "Checking Service Logs"
        Several essential logs generated by system processes, users and administrator actions can be found in `/var/log` directory. Logs can be accessed and viewed using several commands. For example, the `dmesg` command can be used to display the kernel ring buffer. Most system logs are managed by `systemd` and can be checked using the command `journalctl`.
        ```bash
        journalctl
        ```
        > This command will show the entire system log from the boot to the moment you’re calling the journal.
        ```bash
        journalct -u [service_name]
        ```
        > To display logs for a specific service, the `-u` option can be used followed by the service’s name.
        !!! example "Display logs for PosgreSQL"
        ```bash title="journalctl -u postgresql"
        Feb 03 18:03:25 chanvi-Dell-G15-5520 systemd[1]: postgresql.service: Deactivated successfully.
        Feb 03 18:03:25 chanvi-Dell-G15-5520 systemd[1]: Stopped postgresql.service - PostgreSQL RDBMS.
        -- Boot 7e4d6dedb3a84472a4c09dc86fffce33 --
        Feb 03 19:43:29 chanvi-Dell-G15-5520 systemd[1]: Starting postgresql.service - PostgreSQL RDBMS...
        Feb 03 19:43:29 chanvi-Dell-G15-5520 systemd[1]: Finished postgresql.service - PostgreSQL RDBMS.
        Feb 03 20:06:34 chanvi-Dell-G15-5520 systemd[1]: postgresql.service: Deactivated successfully.
        Feb 03 20:06:34 chanvi-Dell-G15-5520 systemd[1]: Stopped postgresql.service - PostgreSQL RDBMS.
        -- Boot 17f7b7cf745a497e8995273fa628f802 --
        Feb 04 08:39:12 chanvi-Dell-G15-5520 systemd[1]: Starting postgresql.service - PostgreSQL RDBMS...
        Feb 04 08:39:12 chanvi-Dell-G15-5520 systemd[1]: Finished postgresql.service - PostgreSQL RDBMS.
        Feb 04 17:57:34 chanvi-Dell-G15-5520 systemd[1]: postgresql.service: Deactivated successfully.
        Feb 04 17:57:34 chanvi-Dell-G15-5520 systemd[1]: Stopped postgresql.service - PostgreSQL RDBMS.
        ...
        -- Boot 84636cdedf26420e8bb1b2170ee71809 --
        Feb 25 08:49:01 chanvi-Dell-G15-5520 systemd[1]: Starting postgresql.service - PostgreSQL RDBMS...
        Feb 25 08:49:01 chanvi-Dell-G15-5520 systemd[1]: Finished postgresql.service - PostgreSQL RDBMS.
        Feb 25 14:21:06 chanvi-Dell-G15-5520 systemd[1]: postgresql.service: Deactivated successfully.
        Feb 25 14:21:06 chanvi-Dell-G15-5520 systemd[1]: Stopped postgresql.service - PostgreSQL RDBMS.
        Feb 25 14:22:12 chanvi-Dell-G15-5520 systemd[1]: Starting postgresql.service - PostgreSQL RDBMS...
        Feb 25 14:22:12 chanvi-Dell-G15-5520 systemd[1]: Finished postgresql.service - PostgreSQL RDBMS.
        Feb 25 14:22:50 chanvi-Dell-G15-5520 systemd[1]: postgresql.service: Deactivated successfully.
        Feb 25 14:22:50 chanvi-Dell-G15-5520 systemd[1]: Stopped postgresql.service - PostgreSQL RDBMS.
        Feb 25 14:22:50 chanvi-Dell-G15-5520 systemd[1]: Stopping postgresql.service - PostgreSQL RDBMS...
        Feb 25 14:22:53 chanvi-Dell-G15-5520 systemd[1]: Starting postgresql.service - PostgreSQL RDBMS...
        Feb 25 14:22:53 chanvi-Dell-G15-5520 systemd[1]: Finished postgresql.service - PostgreSQL RDBMS.
        Feb 25 14:23:09 chanvi-Dell-G15-5520 systemd[1]: postgresql.service: Deactivated successfully.
        Feb 25 14:23:09 chanvi-Dell-G15-5520 systemd[1]: Stopped postgresql.service - PostgreSQL RDBMS.
        Feb 25 14:25:53 chanvi-Dell-G15-5520 systemd[1]: Starting postgresql.service - PostgreSQL RDBMS...
        Feb 25 14:25:53 chanvi-Dell-G15-5520 systemd[1]: Finished postgresql.service - PostgreSQL RDBMS.
        Feb 25 14:28:59 chanvi-Dell-G15-5520 systemd[1]: postgresql.service: Deactivated successfully.
        Feb 25 14:28:59 chanvi-Dell-G15-5520 systemd[1]: Stopped postgresql.service - PostgreSQL RDBMS.
        Feb 25 14:28:59 chanvi-Dell-G15-5520 systemd[1]: Stopping postgresql.service - PostgreSQL RDBMS...
        Feb 25 14:29:02 chanvi-Dell-G15-5520 systemd[1]: Starting postgresql.service - PostgreSQL RDBMS...
        Feb 25 14:29:02 chanvi-Dell-G15-5520 systemd[1]: Finished postgresql.service - PostgreSQL RDBMS.
        lines 159-176/176 (END)
        ```
    ??? question "Creating New Services"
        ```bash title="`my_service.service` file"
        [Unit]
        Description=My Custom Service
        After=network.target

        [Service]
        ExecStart=/path/to/your/executable

        [Install]
        WantedBy=multi-user.target
        ```
        This service file can be placed under `/etc/systemd/system/ `to make systemd recognize it. You would then control the service using `systemctl`, systemd’s command too
        > Note that best practices in Linux dictate that we should not run services as root whenever possible, for security reasons. Instead, we should create a new user to run the service.
??? abstract "Package Management"
    Linux distributions use various package managers. Some of the commonly used are `apt` (Advanced Packaging Tool) for Debian-based distributions, `yum` (Yellowdog Updater, Modified) and `dnf` (Dandified YUM) for Red-Hat-based distributions, and `pacman` for Arch Linux.
    ??? question "Package Repositories"
        A repository in Linux is a storage location from where the system retrieves and installs the necessary OS updates and applications. These repositories contain thousands of Software Packages or RPM Packages compiled for specific Linux distributions.

        The specific repository used depends on the Linux distribution (like Ubuntu, Fedora, etc.) and the package format the distribution uses (like .deb in Debian and Ubuntu or .rpm in Fedora and CentOS).

        Repositories provide a method of updating the tools and applications on your Linux system, and they also ensure all updates and dependencies work together and are tested for integration before they are released.

        There is no standard way to use the repositories across various distributions, each comes with its pre-configured set of repositories.
        ```bash title="Update the repository in Ubuntu"
        sudo apt update
        ```
        ```bash title="Update the repository in CentOS/RHEL/Fedora"
        sudo yum update
        ```
        ```bash title="Update the repository in Racket"
        raco pkg update
        ```
    ??? question "Snap"
        Snap is a modern approach to package management in Linux systems promoted by Canonical (the company behind Ubuntu). Unlike traditional package management systems such as dpkg or RPM, Snap focuses on providing software as self-contained packages (known as ‘Snaps’) that include all of their dependencies. This ensures that a Snap application runs consistently across a variety of different Linux distributions.

        Snaps are installed from a Snapcraft store and are automatically updated in the background. The Snap update process is transactional, meaning if something goes wrong during an update, Snap can automatically revert to the previous working version.
        ```bash title="Example of a snap command"
        sudo snap install [package_name]
        ```
    ??? question "Finding and Installing Packages"
        ```bash title="Install a new package on a Debian-based system like Ubuntu"
        sudo [apt | apt-get] update
        sudo [apt | apt-get] install [package_name]
        ```
        ```bash title="Install a new package on a Fedora/RHEL/CentOS"
        sudo [dnf | yum] update
        sudo [dnf | yum] install [package_name]
        ```
    ??? question "Listing Installed Packages"
        ```bash title="Listing installed packages in an `apt` package manager"
        sudo apt list --installed
        ```
        ```bash title="Listing installed packages for `dnf` package manager"
        dnf list installed
        ```
    ??? question "Install/Remove/Upgrade Packages"
        ```bash title="Remove a package"
        ```
        ```bash title="Update a package"
        ```
??? abstract "Linux Disks Filesystems"
    Linux uses a variety of filesystems to allow us to store and retrieve data from the hardware of a computer system such as disks. The filesystem defines how data is organized, stored, and retrieved on these storage devices. Examples of popular Linux filesystems include EXT4, FAT32, NTFS, and Btrfs.

    Each filesystem has its own advantages, disadvantages, and use cases. For example, EXT4 is typically used for Linux system volumes due to its robustness and compatibility with Linux, while FAT32 may be used for removable media like USB drives for its compatibility with almost all operating systems.
    !!! example "View the Filesystem type"
        ```bash title="df -T"
        Filesystem      Type     1K-blocks    Used Available Use% Mounted on
        udev            devtmpfs    986480       0    986480   0% /dev
        tmpfs           tmpfs       199404     412    198992   1% /run
        /dev/nvme0n1p1  ext4      51359360 8744592  40424004  18% /
        tmpfs           tmpfs       997000       0    997000   0% /dev/shm
        tmpfs           tmpfs         5120       0      5120   0% /run/lock
        /dev/nvme0n1p15 vfat        126678   10922    115756   9% /boot/efi
        tmpfs           tmpfs       199400       0    199400   0% /run/user/0
        ```
    ??? question "Inodes"
        In a Linux filesystem, an inode (index node) is a core concept that represents a filesystem object such as a file or a directory. More specifically, an inode is a data structure that stores critical information about a file except its name and actual data. This information includes the file’s size, owner, access permissions, access times, and more.
        
        Every file or directory in a Linux filesystem has a unique inode, and each inode is identified by an inode number within its own filesystem. This inode number provides a way of tracking each file, acting as a unique identifier for the Linux operating system.

        Whenever a file is created in Linux, it is automatically assigned an inode that stores its metadata. The structure and storage of inodes are handled by the filesystem, which means the kind and amount of metadata in an inode can differ between filesystems.
        !!! example "Retrieve the inode of files/dirs"
        ```bash title="ls -i"
        17859963 directory  17855518 file1.txt  17856147 file2.txt  17845502 file.txt  17831913 sorted_file.txt  17830444 stderr.txt  17827405 stdout.txt
        ```
        ```bash title="ls -i file.txt"
        17845502 file.txt
        ```
    ??? question "Filesystems"
        Linux supports various types of filesystems, such as EXT4, XFS, BTRFS, etc. Each one of them has their own advantages regarding performance, data integrity and recovery options.
        !!! example "View the Filesystem type"
            ```bash title="df -T"
            Filesystem      Type     1K-blocks    Used Available Use% Mounted on
            udev            devtmpfs    986480       0    986480   0% /dev
            tmpfs           tmpfs       199404     412    198992   1% /run
            /dev/nvme0n1p1  ext4      51359360 8744592  40424004  18% /
            tmpfs           tmpfs       997000       0    997000   0% /dev/shm
            tmpfs           tmpfs         5120       0      5120   0% /run/lock
            /dev/nvme0n1p15 vfat        126678   10922    115756   9% /boot/efi
            tmpfs           tmpfs       199400       0    199400   0% /run/user/0
            ```
    ??? question "Mounts"
        In Linux environments, a very crucial concept related to disk management is the “mounting” of filesystems. Fundamentally, mounting in Linux refers to the process that allows the operating system to access data stored on underlying storage devices, such as hard drives or SSDs. This process attaches a filesystem (available on some storage medium) to a specific directory (also known as a mount point) in the Linux directory tree.

        The beauty of this approach lies in the unified and seamless manner in which Linux treats all files, irrespective of whether they reside on a local disk, network location, or any other kind of storage device.

        The `mount` command in Linux is used for mounting filesystems. When a specific filesystem is ‘mounted’ at a particular directory, the system can begin reading data from the device and interpreting it according to the filesystem’s rules.

        It’s worth noting that Linux has a special directory, `/mnt`, that is conventionally used as a temporary mount point for manual mounting and unmounting operations.
        ```bash title="Mount the second partition of a second hard drive at the `/mnt` directory"
        mount /dev/sdb1 /mnt
        ```
    ??? question "Adding Disks"
        !!! note "List all block devices (disk and partitions)."
            ```bash title="lsblk" hl_lines="2"
            NAME                        MAJ:MIN RM   SIZE RO TYPE  MOUNTPOINTS  
            sda                           8:0    1 119.2G  0 disk  
            nvme0n1                     259:0    0 476.9G  0 disk  
            ├─nvme0n1p1                 259:1    0     1G  0 part  /boot/efi
            ├─nvme0n1p2                 259:2    0     2G  0 part  /boot
            └─nvme0n1p3                 259:3    0 473.9G  0 part  
            └─dm_crypt-0              252:0    0 473.9G  0 crypt 
                └─ubuntu--vg-ubuntu--lv 252:1    0 473.9G  0 lvm   /
            ```
        !!! note "Create a new partition on a disk."
            ```bash title="sudo fdisk /dev/sda" hl_lines="5 9-12 16 28"
            Welcome to fdisk (util-linux 2.39.3).
            Changes will remain in memory only, until you decide to write them.
            Be careful before using the write command.

            Command (m for help): n
            Partition type
            p   primary (0 primary, 0 extended, 4 free)
            e   extended (container for logical partitions)
            Select (default p): p
            Partition number (1-4, default 1): 1
            First sector (2048-250068991, default 2048): 
            Last sector, +/-sectors or +/-size{K,M,G,T,P} (2048-250068991, default 250068991): 

            Created a new partition 1 of type 'Linux' and of size 119.2 GiB.

            Command (m for help): p
            Disk /dev/sda: 119.24 GiB, 128035323904 bytes, 250068992 sectors
            Disk model: USB Flash Drive 
            Units: sectors of 1 * 512 = 512 bytes
            Sector size (logical/physical): 512 bytes / 512 bytes
            I/O size (minimum/optimal): 512 bytes / 512 bytes
            Disklabel type: dos
            Disk identifier: 0xbf31f41c

            Device     Boot Start       End   Sectors   Size Id Type
            /dev/sda1        2048 250068991 250066944 119.2G 83 Linux

            Command (m for help): w
            The partition table has been altered.
            Calling ioctl() to re-read partition table.
            Syncing disks.
            ```
            ```bash title="lsblk" hl_lines="3"
            NAME                        MAJ:MIN RM   SIZE RO TYPE  MOUNTPOINTS  
            sda                           8:0    1 119.2G  0 disk  
            └─sda1                        8:1    1 119.2G  0 part  
            nvme0n1                     259:0    0 476.9G  0 disk  
            ├─nvme0n1p1                 259:1    0     1G  0 part  /boot/efi
            ├─nvme0n1p2                 259:2    0     2G  0 part  /boot
            └─nvme0n1p3                 259:3    0 473.9G  0 part  
            └─dm_crypt-0              252:0    0 473.9G  0 crypt 
                └─ubuntu--vg-ubuntu--lv 252:1    0 473.9G  0 lvm   /
            ```
        !!! note "Create a new filesystem on a partition." 
            ```bash title="sudo mkfs.ext4 /dev/sda1" hl_lines="8-11"
            mke2fs 1.47.0 (5-Feb-2023)
            Creating filesystem with 31258368 4k blocks and 7815168 inodes
            Filesystem UUID: 7dba2cd1-a61f-4139-adb2-a3c21df3abd0
            Superblock backups stored on blocks: 
                    32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632, 2654208, 
                    4096000, 7962624, 11239424, 20480000, 23887872

            Allocating group tables: done                            
            Writing inode tables: done                            
            Creating journal (131072 blocks): done
            Writing superblocks and filesystem accounting information: done
            ```
        !!! note "Mount a filesystem to a directory."
            ```bash title="sudo mount /dev/sda1 /mnt"
            ```
            ```bash title="lsblk" hl_lines="3"
            NAME                        MAJ:MIN RM   SIZE RO TYPE  MOUNTPOINTS  
            sda                           8:0    1 119.2G  0 disk  
            └─sda1                        8:1    1 119.2G  0 part  /mnt
            nvme0n1                     259:0    0 476.9G  0 disk  
            ├─nvme0n1p1                 259:1    0     1G  0 part  /boot/efi
            ├─nvme0n1p2                 259:2    0     2G  0 part  /boot
            └─nvme0n1p3                 259:3    0 473.9G  0 part  
            └─dm_crypt-0              252:0    0 473.9G  0 crypt 
                └─ubuntu--vg-ubuntu--lv 252:1    0 473.9G  0 lvm   /
            ```
            ```bash title="df -T" hl_lines="9"
            Filesystem      Type     1K-blocks    Used Available Use% Mounted on
            udev            devtmpfs    986480       0    986480   0% /dev
            tmpfs           tmpfs       199404     412    198992   1% /run
            /dev/nvme0n1p1  ext4      51359360 8744592  40424004  18% /
            tmpfs           tmpfs       997000       0    997000   0% /dev/shm
            tmpfs           tmpfs         5120       0      5120   0% /run/lock
            /dev/nvme0n1p15 vfat        126678   10922    115756   9% /boot/efi
            tmpfs           tmpfs       199400       0    199400   0% /run/user/0
            /dev/sda1       ext4     122485360      24 116217280   1% /mnt
            ```
    ??? question "Swap"
        Swap space in Linux is used when the amount of physical memory (RAM) is full. If the system needs more memory resources and the physical memory is full, inactive pages in memory are moved to the swap space. Swap space is a portion of a hard disk drive (HDD) that is used for virtual memory.

        Having swap space ensures that whenever your system runs low on physical memory, it can move some of the data to the swap, freeing up RAM space, but this comes with performance implications as disk-based storage is slower than RAM.

        In the context of disks and filesystems, the swap space can live in two places:

        1. In its own dedicated partition.
        2. In a regular file within an existing filesystem.

        ```bash
        fallocate -l 1G /swapfile # creates a swap file
        chmod 600 /swapfile # secures the swap file by preventing regular users from reading it
        mkswap /swapfile # sets up the Linux swap area
        swapon /swapfile # enables the file for swapping
        ```
    ??? question "LVM"
        The Linux Logical Volume Manager (LVM) is a device mapper framework that provides logical volume management for the Linux kernel. It was created to ease disk management, allowing for the use of abstracted storage devices, known as logical volumes, instead of using physical storage devices directly.

        LVM is extremely flexible, and features include resizing volumes, mirroring volumes across multiple physical disks, and moving volumes between disks without needing to power down.

        LVM works on 3 levels: Physical Volumes (PVs), Volume Groups (VGs), and Logical Volumes (LVs).

        1. PVs are the actual disks or partitions.
        2. VGs combine PVs into a single storage pool.
        3. LVs carve out portions from the VG to be used by the system.

        ```bash title="create an LVM"
        pvcreate /dev/sdb1
        vgcreate my-vg /dev/sdb1
        lvcreate -L 10G my-vg -n my-lv
        ```
??? abstract "Booting Linux"
    The whole process involves several stages including POST (Power-On Self Test), MBR (Master Boot Record), GRUB (GRand Unified Bootloader), Kernel, Init process, and finally the GUI or command line interface where users interact.

    During this process, vital system checks are executed, hardware is detected, appropriate drivers are loaded, filesystems are mounted, necessary system processes are started, and finally, the user is presented with a login prompt.
    ```bash title="example of the GRUB configuration file `/etc/default/grub`"
    GRUB_DEFAULT=0
    GRUB_TIMEOUT=5
    GRUB_DISTRIBUTOR=`lsb_release -i -s 2> /dev/null || echo Debian`
    GRUB_CMDLINE_LINUX_DEFAULT="quiet splash"
    GRUB_CMDLINE_LINUX=""
    ```
    ??? question "Boot Loaders"
    ??? question "Logs"
??? abstract "Networking"
    ??? question "TCP/IP Stack"
    ??? question "Subnetting"
    ??? question "Ethernet & ARP/RARP"
    ??? question "DHCP"
    ??? question "IP Routing"
    ??? question "DNS Resolution"
    ??? question "Netfilter"
    ??? question "SSH"
    ??? question "File Transfer"
??? abstract "Backup Tools"
    ??? question "rsync"
    ??? question "tar"
    ??? question "dump"
    ??? question "restore"
??? abstract "Shell Programming"
    ??? question "Variables"
    ??? question "Literals"
    ??? question "Loops"
    ??? question "Conditionals"
    ??? question "Debugging"
??? abstract "Troubleshooting"
    ??? question "ping"
    ??? question "ICMP"
    ??? question "traceroute"
    ??? question "netstat"
    ??? question "Packet Analysis"
??? abstract "Containerization"
    ??? question "ulimits"
    ??? question "cgroups"
    ??? question "Container Runtime"
    ??? question "Docker"
</div>
