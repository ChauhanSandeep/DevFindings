---
title: "A Developer's Guide to Essential Terminal Commands"
datePublished: Sat Oct 11 2025 12:30:53 GMT+0000 (Coordinated Universal Time)
cuid: cmgm97kxo000102lb0wmsfpev
slug: a-developers-guide-to-essential-terminal-commands

---

This guide provides a curated list of essential commands for `Git`, the `GitHub CLI`, and your `Terminal`. Each command includes a breakdown of its arguments to help you understand what's happening and how to use them effectively in your daily workflow.

## 🐙 Git Commands

### 1\. Everyday Workflow & Inspection

* **Check Status**: Get a compact, single-line overview of your repository's status.
    
    Bash
    
    ```bash
    git status -s 
    ```
    
    * `-s` or `--short`: Provides output in a short, easy-to-read format. `M` means modified, `A` means added, `??` means untracked, etc.
        
* **Power Log**: View a condensed, graph-based log of all commits across all branches.
    
    Bash
    
    ```bash
    git log --oneline --graph --decorate --all
    ```
    
    * `--oneline`: Condenses each commit to a single line (hash and commit message).
        
    * `--graph`: Draws a text-based graph showing the branch structure.
        
    * `--decorate`: Shows branch names, tags, and other references pointing to commits.
        
    * `--all`: Displays commits from all branches, not just the current one.
        
* **View Unstaged Changes**: See the differences between your working directory and the last commit (what you *could* stage).
    
    Bash
    
    ```bash
    git diff
    ```
    
* **View Staged Changes**: See the differences between your staged changes and the last commit (what you are *about to* commit).
    
    Bash
    
    ```bash
    git diff --staged
    ```
    
    * `--staged` or `--cached`: Shows changes that have been added to the index via `git add`.
        
* **Interactive Staging**: Interactively review and stage portions (or "hunks") of code from your modified files instead of staging the entire file.
    
    Bash
    
    ```bash
    git add -p
    ```
    
    * `-p` or `--patch`: Enters an interactive mode where Git shows you each change and asks if you want to stage it (`y`), skip it (`n`), split it into smaller changes (`s`), etc.
        
* **Verbose Commit**: Open your text editor to write a commit message, but also include the full diff of your changes in the editor as a comment for context.
    
    Bash
    
    ```bash
    git commit -v
    ```
    
    * `-v` or `--verbose`: Helps you write more accurate commit messages by showing you exactly what you've changed.
        

### 2\. Branching & History Manipulation

* **Switch Branches**: The modern, intuitive command to switch between existing branches.
    
    Bash
    
    ```bash
    git switch <branch-name>
    ```
    
* **Create and Switch to a New Branch**: A single command to create a new branch from your current position and immediately switch to it.
    
    Bash
    
    ```bash
    git switch -c <new-branch-name>
    ```
    
    * `-c` or `--create`: The flag that tells Git to create a new branch.
        
* **Interactive Rebase**: The ultimate tool for cleaning up commit history. It opens an editor allowing you to reorder, squash (combine), edit, or remove recent commits before merging.
    
    Bash
    
    ```bash
    git rebase -i main
    ```
    
    * `-i` or `--interactive`: Enters the interactive mode.
        
    * `main`: The target branch. This command rewrites the history of your current branch *on top of* `main`.
        
* **Cherry Pick**: Apply a specific commit from another branch to your current branch.
    
    Bash
    
    ```bash
    git cherry-pick <commit-hash>
    ```
    
    * `<commit-hash>`: The unique identifier of the commit you want to copy over.
        
* **Hard Reset**: **DANGER!** Discards your last commit *and* all the changes in your working directory associated with it. Use with extreme caution.
    
    Bash
    
    ```bash
    git reset --hard HEAD~1
    ```
    
    * `--hard`: Resets the commit history, the staging area, AND your working directory.
        
    * `HEAD~1`: Refers to the commit just before the current one (`HEAD`).
        
* **Soft Reset**: Undoes the last commit but keeps all the changes from that commit in your staging area, ready to be re-committed.
    
    Bash
    
    ```bash
    git reset --soft HEAD~1
    ```
    
    * `--soft`: Resets the commit history only, leaving your files and staging area untouched.
        
* **Reflog**: Your safety net. It shows a log of every movement `HEAD` has made. If you ever mess up a rebase or reset, `reflog` is how you can find your "lost" commits and restore them.
    
    Bash
    
    ```bash
    git reflog
    ```
    

### 3\. Working with Remotes

* **Fetch**: Download all the latest changes (commits, branches, tags) from the remote repository but **does not** merge them into your local branches.
    
    Bash
    
    ```bash
    git fetch
    ```
    
* **Pull with Rebase**: The recommended way to update your local branch. It fetches remote changes and then "re-plays" your local commits on top of the latest remote version, maintaining a clean, linear history.
    
    Bash
    
    ```bash
    git pull --rebase
    ```
    
* **Force Push with Lease**: A safer way to force push. It will fail if someone else has pushed new commits to the remote branch since you last fetched, preventing you from accidentally overwriting their work.
    
    Bash
    
    ```bash
    git push --force-with-lease
    ```
    
* **Push and Set Upstream**: Push a new local branch to the remote and configure it to track the remote branch. This lets you use `git pull` and `git push` without extra arguments in the future.
    
    Bash
    
    ```bash
    git push -u origin <branch-name>
    ```
    
    * `-u` or `--set-upstream`: Creates the tracking connection between your local branch and the new remote branch.
        

---

## 🚀 GitHub CLI (`gh`): Your Superpower

The GitHub CLI brings GitHub to your terminal, saving you from switching to the browser.

### 1\. The Pull Request Workflow

* **Create a PR**: Interactively create a pull request from your current branch. `gh` will prompt you for the title, body, reviewers, and more.
    
    Bash
    
    ```plaintext
    gh pr create
    # Or with flags:
    gh pr create --title "My PR Title" --body "Details here" --reviewer "username"
    ```
    
* **List PRs**: See a list of open pull requests in the repository.
    
    Bash
    
    ```plaintext
    gh pr list
    ```
    
* **Checkout a PR**: Download the code from a specific pull request into a new local branch so you can test it.
    
    Bash
    
    ```plaintext
    gh pr checkout <pr-number>
    ```
    
* **View PR Diff**: See the file changes for a specific PR directly in your terminal.
    
    Bash
    
    ```plaintext
    gh pr diff <pr-number>
    ```
    
* **Review a PR**: Start an interactive session to approve, comment on, or request changes for a pull request.
    
    Bash
    
    ```plaintext
    gh pr review <pr-number>
    ```
    
* **Merge a PR**: Merge a pull request from the command line.
    
    Bash
    
    ```plaintext
    gh pr merge <pr-number> --squash --delete-branch
    ```
    
    * `--squash`: Combines all commits in the PR into a single commit on the base branch.
        
    * `--delete-branch`: Deletes the remote branch after merging.
        

### 2\. Other Handy `gh` Commands

* **Clone a Repo**: A simpler way to clone a repository you have access to.
    
    Bash
    
    ```plaintext
    gh repo clone <owner/repo>
    ```
    
* **View Repo in Web**: Quickly open the current repository's GitHub page in your default web browser.
    
    Bash
    
    ```plaintext
    gh repo view -w
    ```
    
    * `-w` or `--web`: Specifies opening in the web browser.
        
* **List Issues**: View and filter the project's issues.
    
    Bash
    
    ```plaintext
    gh issue list
    ```
    
* **List Action Runs**: Check the status of your GitHub Actions CI/CD runs.
    
    Bash
    
    ```plaintext
    gh run list
    ```
    

---

## 💻 Terminal Commands (Linux/macOS)

### 1\. Navigation & Directory Management

* `ls` – List Files: Lists files and directories.
    
    Bash
    
    ```plaintext
    ls -lh
    ```
    
    * `-l`: Long listing format (shows permissions, owner, size, date).
        
    * `-h`: Human-readable sizes (e.g., `4.0K`, `1.2M`).
        
    * `-a`: Shows all files, including hidden dotfiles (e.g., `.bashrc`).
        
    * `-t`: Sorts by modification time, newest first.
        
    * `-R`: Recursively lists subdirectories.
        
* `tree` – Display Directory Structure: Visualizes the folder hierarchy as a tree. (May need to be installed: `sudo apt install tree` or `brew install tree`).
    
    Bash
    
    ```plaintext
    tree -L 2 
    ```
    
    * `-L 2`: Limits the depth of the tree to 2 levels.
        
* `find` – Search for Files: A powerful tool to locate files.
    
    Bash
    
    ```plaintext
    find . -name "*.java"
    ```
    
    * `.`: The path to search in (current directory).
        
    * `-name "*.java"`: The expression to match (any file ending in `.java`).
        
    * `-type f`: Find only files.
        
    * `-type d`: Find only directories.
        
    * `-mtime -1`: Find files modified in the last 24 hours.
        

### 2\. File Viewing & Manipulation

* `cat` – View File Contents: Prints the entire content of a file to the screen.
    
    Bash
    
    ```plaintext
    cat file.txt
    ```
    
* `less` – Paginated File Viewer: View large files page by page. Use arrow keys to navigate and `q` to quit. Much better than `cat` for large log files.
    
    Bash
    
    ```plaintext
    less app.log
    ```
    
* `head` and `tail`: Preview the beginning or end of a file.
    
    Bash
    
    ```plaintext
    tail -n 50 app.log
    tail -f app.log 
    ```
    
    * `-n 50`: Shows the last 50 lines.
        
    * `-f`: "Follow" mode. Continuously outputs new lines as they are added to the file, great for watching live logs.
        
* `grep` – Search Within Files: Find lines containing a specific pattern.
    
    Bash
    
    ```plaintext
    grep -r "LinkedInService" src/
    ```
    
    * `-r` or `-R`: Recursive search through a directory.
        
    * `-i`: Case-insensitive search.
        
    * `-v`: Invert match; shows lines that *do not* contain the pattern.
        
    * `--line-buffered`: Useful when piping from a command like `tail -f`.
        

### 3\. System & Process Management

* `ps` – Process Status: List currently running processes. Often used with `grep` to find a specific one.
    
    Bash
    
    ```plaintext
    ps aux | grep java
    ```
    
    * `aux`: A common set of flags to show all processes (`a`), including those without a terminal (`x`), with user details (`u`).
        
* `kill` – Terminate a Process: Send a signal to a process (identified by its PID) to terminate it.
    
    Bash
    
    ```plaintext
    kill 12345
    kill -9 12345
    ```
    
    * By default, `kill` sends a `TERM` signal, asking the process to shut down gracefully.
        
    * `-9`: Sends the `KILL` signal, which is non-blockable and forces the process to terminate immediately. Use this as a last resort.
        
* `df` – Disk Usage: Report file system disk space usage.
    
    Bash
    
    ```plaintext
    df -h
    ```
    
    * `-h`: Human-readable format (e.g., `GB`, `MB`).
        
* `du` – Directory Size: Show the disk usage of files and directories.
    
    Bash
    
    ```plaintext
    du -sh *
    ```
    
    * `-s`: Summarize, showing a total for each argument.
        
    * `-h`: Human-readable format.
        

### 4\. Networking

* `ss` – Socket Statistics: A modern replacement for `netstat` that displays network connection information.
    
    Bash
    
    ```plaintext
    ss -tulpn
    ```
    
    * `-t`: Show TCP sockets.
        
    * `-u`: Show UDP sockets.
        
    * `-l`: Show only listening sockets.
        
    * `-p`: Show the process using the socket.
        
    * `-n`: Do not resolve service names (show port numbers).
        
* `lsof` – List Open Files: A powerful debugging tool to see which process is using a specific file or port.
    
    Bash
    
    ```plaintext
    lsof -i :8080
    ```
    
    * `-i :8080`: Shows the process listening on port 8080.
        

### 5\. Shell Power-Ups

* **Piping** `|`: Use the output of one command as the input for another.
    
    Bash
    
    ```bash
    # Find all Java processes, then count them
    ps aux | grep java | wc -l
    ```
    
* **Redirection** `>` & `>>`: Send the output of a command to a file.
    
    Bash
    
    ```bash
    # Overwrite files.txt with the list of files
    ls -l > files.txt 
    
    # Append the list of files to files.txt
    ls -l >> files.txt 
    ```
    
* `xargs` – Execute Arguments: Takes items from standard input and passes them as arguments to another command.
    
    Bash
    
    ```bash
    # Find all .tmp files and delete them
    find . -name "*.tmp" | xargs rm
    ```
    
* `tee` – Split Output: Reads from standard input and writes to both standard output and one or more files simultaneously.
    
    Bash
    
    ```bash
    # Run the deploy script, see the output on screen, AND save it to deploy.log
    ./deploy.sh | tee deploy.log
    ```