# Git & GitHub

### **INDEX**

- Introduction
- Installation
- Basic Git Operations
    - Stage & Commit Changes
    - Modifying & Re-Committing files
    - Restoring Staged Changes & Deletion
    - View Commit History
    - Stashing Changes
    - Popping Stash
    - Clearing Stash
- Publish local Repository over Github

---

### **Introduction**

**Git** : Git is a distributed version control system used to track changes in source code during software development. It allows multiple developers to work on a project simultaneously, manage code history, collaborate, and revert to previous versions of code when needed. Created by **Linus Torvalds** in 2005.

**GitHub** : GitHub is a web-based platform that hosts Git repositories online. It provides a collaborative environment for developers to store, share, and manage their Git-based projects, with additional tools for issue tracking, code review, CI/CD, and team collaboration. Acquired by Microsoft in 2018.

---

### **Installation**

Git Installation Link: [https://git-scm.com/](https://git-scm.com/)

- Run the Installer and setup the env
- Launch Git  Bash
- Installation Verification
    
    ```bash
    git --version
    ```
    

---

### **Initializing Git Repository**

**What is a Git Repository?**

A Git repo (repository) is a virtual storage of your project. It tracks all changes made to files and allows you to collaborate with others. You can create a Git repository either locally (on your computer) or remotely (like on GitHub).

**Steps :** 

- Open Terminal
- Navigate project folder
- Initialization command
    
    ```bash
    git init
    ```
    
- An Empty repository is successfully created

**Example:**

```bash
mkdir new-project
cd new-project
git init
```

---

### **Basic Git Operations**

**Stage & Commit Changes**

- **Step by Step Guide**
    - Create or Edit File
        
        ```bash
        echo "Hello User" > Testing.txt
        ```
        
    - Check Status
        
        
        ```bash
        git status
        ```
        
        This will show the Untracked files i.e., changed but not committed
        
        ```bash
        Untracked files:
          (use "git add <file>..." to include in what will be committed)
            Testing.txt
        ```
        
    - Stage File
        
        ```bash
        git add Testing.txt
        ```
        
    - Commit Changes
        
        ```bash
        git commit -m "Add Testing.txt with greeting message"
        ```
        

**Summarized Example:** 

```bash
echo "Hello User" > Tesing.txt     # Create a file
git status                       # Check file status
git add Tesing.txt                # Stage the file
git commit -m "Add Tesing.txt"    # Commit the file
```

**Modifying & Re-Committing files**

- After adding more content to Testing.txt
- Check Status using git status command again
    
    ```bash
    Changes not staged for commit:
      (use "git add <file>..." to update what will be committed)
        modified:   Testing.txt
    ```
    
- Stage & Commit changes
    
    ```bash
    git add Testing.txt
    git commit -m "Update Testing.txt with additional info"
    ```
    

**Restoring Staged Changes & Deleting files**

- Restore a Modified File to Last Commit: 
This will remove all uncommitted changes in `Testing.txt` and revert it to the version in your last commit.
    
    ```bash
    git restore Testing.txt
    ```
    
- Unstage Staged File: The file will stay in your working directory, but Git will stop tracking it in the staging area.
    
    ```bash
    git restore --staged Testing.txt
    ```
    
- Restore All Files: 
This will discard **all local changes** that are not committed!
    
    ```bash
    git restore --staged Testing.txt
    ```
    
- Deleting File: Deleting whole file from the project
    
    ```bash
    rm filename.ext    #Deleting Single file
    rm file1.txt file2.txt file3.txt   #Deleting multiple files
    rm *.log     #Deleting all files with same extention
    rm -rf foldername/   #Deleting Directory and Its Contents
    ```
    

**View Commit History** 

- Basic Git log: To view the commit history with Author details who made the commit.
    
    ```bash
    git add Testing.txt
    git commit -m "Update Testing.txt with additional info"
    ```
    
- Compact One-Line Log: For a simpler, more concise log.
    
    ```bash
    git log --oneline
    ```
    
- Graph View of Branches: To view the commit history as a **branch graph**
    
    ```bash
    git log --oneline --graph --all
    ```
    
- Filtering Logs: can filter log history based on basic specifications
    - Author
        
        ```bash
        git log --author="Devashish"
        ```
        
    - Since / Until Date
        
        ```bash
        git log --since="2 days ago"
        git log --until="2024-12-01"
        ```
        
    - Specific File
        
        ```bash
        git log -- Testing.txt
        ```
        

**Stashing Changes**

**Stash**: Temporarily save uncommitted changes so you can work on something else.

```bash
git stash
```

This will save the changes and revert your working directory to the last commit.

**Popping Stash**

**Pop**: Reapply the most recent stash and remove it from the stash list.

```bash
git stash pop
```

If you have multiple stashes, you can apply a specific one:

```bash
git stash list
# Example: stash@{1}
git stash pop stash@{1}
```

**Clearing Stash**

Clear: Remove all Stashed entries entirely. This is irreversible so use with caution

```bash
git stash clear
```

---

### **Publish local Repository over Github**

**Push to GitHub**: To connect your local Git repository to a remote GitHub repository and push your changes

- Browse to GitHub https://github.com/
- Click on New Repository and create one
- Provide repo name and other necessary details like Private/Public
- Do not initialize with README (you already have local content)
- Add the remote URL using:
    
    ```bash
    git remote add origin https://github.com/your-username/my-project.git
    ```
    
- Push Code to GitHub
    
    ```bash
    git push -u origin main
    ```
    
- Change Remote URL : If you need to change the GitHub URL later:
    
    ```bash
    git remote set-url origin https://github.com/your-username/new-repo.git
    ```