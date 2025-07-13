# Git & GitHub InDepth Guide 

### **Content**

- Branch
  - Creating new Branch & Switching
  - Listing Branches
  - Merge Branch & Push

---

### Branch

A branch in Git is a parallel version of your repository. It allows you to work on features, bug fixes, or experiments in isolation without affecting the main codebase. Once the changes are ready, they can be merged back into the main branch. By default, Git creates a branch called `main` or `master` when you initialize a repository.

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