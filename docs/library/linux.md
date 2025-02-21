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
    ??? question "paste"
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

    ??? question "Process Signals"

    ??? question "Process Priorities"

    ??? question "Killing Processes"

    ??? question "Process Forking"

??? abstract "User Management"
??? abstract "Service Management(systemd)"
??? abstract "Package Management"
??? abstract "Linux Disks Filesystems"
??? abstract "Booting Linux"
??? abstract "Networking"
??? abstract "Backup Tools"
??? abstract "Shell Programming"
??? abstract "Troubleshooting"
??? abstract "Containerization"
</div>
