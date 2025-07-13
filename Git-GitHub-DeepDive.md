# Git & GitHub InDepth Guide 

### **Content**

- Branch
  - Creating new Branch & Switching
  - Listing Branches
  - Merge Branch & Push
- Forking & Pull Requests
  - Fork
  - Clone Forked Project Locally
- Upstream
  - Adding Upstream
- Pull Request
  - Create First Pull Request
  - Removing Commit from Pull Request
  - Merge Pull Request
- Squashing Commits
- Rebase Command
- Hard Reset
- Merge Conflicts & Resolution

---

### Branch

A `branch` in Git is a parallel version of your repository. It allows you to work on features, bug fixes, or experiments in isolation without affecting the main codebase. Once the changes are ready, they can be merged back into the main branch. By default, Git creates a branch called `main` or `master` when you initialize a repository.

**Why do we need Branches?**

Branches allow safe collaboration and experimentation. Key benefits:

- Work on features independently
- Avoid conflicts with stable code
- Test and develop without breaking `main`
- Collaborate via feature branches before merging

**Creating a New Branch & Switching to It**

```bash
git branch features      #Create a new Branch
git checkout features    #Switch to new Branch

git checkout -b feature-1  #Create & Switch altogether
```

**Listing Branches** 

Viewing all Branches and Highlight the current active Branch

```bash
git branch          #List all Branches
```

**Merging Branch into Main Branch** 

```bash
git checkout main         #Switch to Main Branch
git merge features        #Merge Branch into Main Branch
```

**Final Pushing Merged Changes**

```bash
git push origin main     #Switch to Main Branch as Active Branch
```

---

### **Forking & Pull Requests**

**Fork** : A **fork** is a personal copy of someone else's repository. Forking allows you to experiment with changes without affecting the original project. It’s commonly used in open-source workflows where you contribute via pull requests.

**Why Do We Use Fork?**

- To contribute to a repository you don’t own.
- To freely try changes without breaking the main project.
- To collaborate on features before proposing them to the main repo.

**Clone Forked Project Locally** 

After you’ve Forked a repo on GitHub :

- Copy the HTTPS/SSH URL from your fork.
- Clone it to your local system:
    
    ```bash
    git clone https://github.com/your-username/forked-repo.git
    cd forked-repo
    ```   

---

### **Upstream : Adding Upstream (Original Repo)**

When you fork a repository, your copy (fork) lives in your own GitHub account. However, the **original repository** continues to receive updates and commits — your fork does **not** automatically get those changes. To stay in sync with the original project, you add a reference to it in your local repo called `upstream`. This lets you **fetch changes** from the original repository and **merge** them into your fork.

- **Add Original repo as Upstream**
    
    ```bash
    git remote add upstream https://github.com/original-user/original-repo.git
    ```
    
- Confirmation
    
    ```bash
    git remote -v    #shows both origin(fork) upstream(original)
    ```
    
---

### **Pull Request**

A **Pull Request (PR)** is a way to propose changes you've made in your fork to the original repository. It's the core of collaborative development on GitHub.

> Note: Always create a new branch for your changes. Never commit directly to the main branch.
> 

**Example: Create First Pull Request**

- Create and switch to a new branch:
    
    ```bash
    git checkout -b feature-branch
    ```
    
- Make changes → Stage → Commit:
    
    ```bash
    git add .
    git commit -m "Added feature"
    ```
    
- Push to your fork:
    
    ```bash
    git push origin feature-branch
    ```
    
- Go to forked repo on GitHub & Click “Compare & Pull request”

---

### **Removing Commit from Pull Request**

If you accidentally committed something, This updates the pull request without the unwanted commit.

```bash
git reset --hard HEAD~1        # Reverts the last commit
git push origin feature-branch --force
```

---

### **Merge Pull Request**

Once the Pull Request (PR) is **reviewed and approved**, it can be merged into the main branch.

- The repo owner (or you if it’s you own repo) can merge it into main.
- Use **“Merge pull request”** on GitHub & Confirm merge.

After merging, delete the feature branch (optional but recommended).

Bash Method / Manual Method:

```bash
git fetch origin    #Fetch all branches including PRs
git checkout main   #Checkout branch you want to merge into
git merge feature-branch-name
git push origin main  #Push Changes to GitHub
```

---

### **Squashing Commits**

Squashing means combining multiple commits into one. It's useful for cleaning up commit history before pushing changes or creating a pull request.

- **Interactive Rebase to Squash Commits**
    
    ```bash
    git rebase -i HEAD~3    # Rebase last 3 commits
    ```
    

This opens an editor like:

  ```bash
  pick 123abc First commit
  pick 456def Second commit
  pick 789ghi Third commit
  ```

Change it to:

```bash
pick 123abc First commit
squash 456def Second commit
squash 789ghi Third commi
```

Save & close. Then provide a new combined commit message.

Finally, force push the updated history:

```bash
git push origin feature-branch --force
```

---

### **Rebase Command**

Rebase is used to move or combine a sequence of commits to a new base commit. It's useful for keeping commit history linear and clean.

- **Example: Rebase feature onto main**
    
    ```bash
    git checkout feature
    git rebase main
    ```
    

If there are no conflicts, feature branch is rebased cleanly on top of main.

If conflicts occur, Git will stop and ask you to resolve them.

After resolving conflicts:

```bash
git add .
git rebase --continue
```

---

### **Hard Reset**

git reset --hard discards changes in your working directory and index — use cautiously.

- **Reset to last commit** (delete all local changes):
    
    ```bash
    git reset --hard HEAD
    ```
    
- **Reset to specific commit:**
    
    ```bash
    git reset --hard <commit-hash>
    ```
    

This will delete all changes permanently unless backed up. If pushed, force push is required:

```bash
git push origin branch-name --force
```

---

### **Merge Conflicts & Resolution**

Merge conflicts occur when Git can’t automatically reconcile differences between two branches.

- **How to Identify Conflict**

During merge or rebase, Git will stop with a message:

```bash
CONFLICT (content): Merge conflict in file.txt
```

- **Steps to Resolve Conflict:**
    - Open the conflicted file and look for conflict markers:
        
        ```markdown
        <<<<<<< HEAD
        Your current changes
        =======
        Incoming branch changes
        >>>>>>> feature-branch
        ```
        
    - Edit and keep only the correct/final version of the code.
    - Stage resolved files:
        
        ```bash
        git add file.txt
        ```
        
    - Complete the merge or rebase:
        
        ```bash
        git commit                         #For merge
        git rebase --continue              #For rebase
        
        ```