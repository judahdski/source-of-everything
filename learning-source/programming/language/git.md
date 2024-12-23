# Git Command Guide

This guide provides a summary of commonly used Git commands, categorized for quick reference.

## Common Usage Commands
- **Stage Changes:**
  ```bash
  git add .
  git add <filename>
  ```
  Stages all changes or specific file(s) for commit.

- **Commit Changes:**
  ```bash
  git commit -m '<message here>'
  ```
  Saves changes with a descriptive message.

- **Push Changes to Remote Repository:**
  ```bash
  git push <remote-name|origin> <branch-name|master>
  ```

- **Pull Changes from Remote Repository:**
  ```bash
  git pull <remote-name|origin> <branch-name|master>
  ```

- **Check Repository Status:**
  ```bash
  git status
  ```
  Displays the current state of the working directory and staging area.

- **View Commit History:**
  ```bash
  git log
  ```
  Shows the commit history.

## Remote Commands
- **Clone a Repository:**
  ```bash
  git clone <url>
  ```
  Downloads a repository from a remote URL.

## Branch Management
- **List Branches:**
  ```bash
  git branch
  ```
  Displays all local branches.

- **Create a New Branch:**
  ```bash
  git branch <branch-name>
  ```

- **Create a Branch from Remote:**
  ```bash
  git branch <branch-name> <remote-name|origin>/<remote-branch-name>
  ```

- **Switch and Create New Branch Simultaneously:**
  ```bash
  git switch -c <branch-name>
  ```

- **Rename a Branch:**
  ```bash
  git branch -c <branch-name>
  ```

- **Restore a File:**
  ```bash
  git restore <file-name>
  ```
  Discards changes in a file and restores it from the last commit.

## Authentication Commands
- **List Stored Credentials:**
  ```bash
  git-credential-manager github list
  ```

- **Login to GitHub:**
  ```bash
  git-credential-manager github login
  ```

- **Logout from GitHub:**
  ```bash
  git-credential-manager github logout <user-name>
  ```