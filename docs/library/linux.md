# 

## Linux 101

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
            * THe last group of three characters: represents the permission for the others. (`r--`)

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
        awk '{print $1,$2}' filename # (1)!
        ```

        1. This would display the first and second field (typically separated by spaces) of every line in ‘filename’.
    ??? question "grep"
        

</div>
