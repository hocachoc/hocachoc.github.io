---
draft: false
date:
  created: 2025-03-02
categories:
  - Linux 🌶️
authors:
  - nhamchanvi
comments: true
---

# Linux Treasure Hunt

This project is more than just a game; it's a practical way to hone your Linux command-line skills, which are essential for any aspiring DevOps engineer. Think of it as an adventure with real-world applications.

[![Image]](#)

[Image]: ../../assets/linux-treasure-hunt-100.jpg

<!-- more -->

## The Challenge:

### 1. Bury the Treasure:

Create a file with a "secret message" (e.g., a fake API key, a server configuration setting, or even a fun message). Hide this file deep within your Linux file system. Get creative with the file name and location!

### 2. Craft the Script:

Write a shell script that uses the find command, along with other Linux commands, to locate your hidden treasure. Consider using:

- find with various options (e.g., -name, -type, -mtime)
- grep to search for specific content within files
- awk or sed for more advanced text processing
- Control flow (e.g., if, else) to handle different scenarios

### 3. Level Up:

- Add a timer to your script to track how long it takes to find the treasure.
- Modify the script to search for multiple treasures.
- Create a "treasure map" (a text file with clues) that your script can decipher to find the treasure.

## Why This Matters for DevOps:

- **File System Mastery**: DevOps engineers often work with complex file systems and need to locate and manage files efficiently.
- **Automation**: Automating tasks with shell scripts is a core DevOps skill. This project gives you hands-on practice.
- **Problem-Solving**: This challenge encourages you to think creatively and use Linux commands in new ways to solve a problem.
- **Security Awareness**: By hiding and finding files, you gain a better understanding of file permissions and security implications, which are crucial in DevOps.

!!! example
    ```bash title="cat my_hidden_treasure.txt"
    super super secret
    ```
    ```bash title="cat treasure_hunt.sh"
    #!/bin/bash

    # Start the timer
    start_time=$(date +%s)

    # Use find to locate the treasure file
    treasure_file=$(find / -name "my_hidden_treasure.txt" 2>/dev/null)

    # Check if the treasure was found
    if [ -n "$treasure_file" ]; then
      echo "Treasure found: $treasure_file"
      cat "$treasure_file"
    else
      echo "Treasure not found!"
    fi

    # Calculate and display the elapsed time
    end_time=$(date +%s)
    elapsed_time=$((end_time - start_time))
    echo "Elapsed time: $elapsed_time seconds"
    ```
    ```bash title="chmod +x treasure_hunt.sh"
    ```
    ```bash title="./treasure_hunt.sh"
    Treasure found: /home/chanvi/learn-devops/learn-linux-sensitive-variables/my_hidden_treasure.txt
    super super secret
    Elapsed time: 5 seconds
    ```
