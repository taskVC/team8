# Git Stash – Detailed Explanation

## 1. Introduction

**Git Stash** is a feature in the version control system **Git** that allows developers to **temporarily save (stash) uncommitted changes** in their working directory without committing them.

This is useful when you need to **switch branches or pull new changes** but your current work is not ready to commit.

Instead of committing incomplete work, you can **stash it**, work on something else, and later **restore your changes**.

---

# 2. Why Git Stash is Used

Sometimes developers are working on a feature but suddenly need to:

* Fix a **bug in another branch**
* Pull updates from the remote repository
* Switch branches quickly

But **Git does not allow branch switching when there are conflicting uncommitted changes**.

Git Stash solves this by:

1. Saving your current modifications.
2. Cleaning your working directory.
3. Allowing you to switch branches safely.

Example scenario:

```
You are working on Feature A
But a critical bug appears in production
You must switch to the bug-fix branch
```

Solution:

```
git stash
git checkout bug-fix
```

---

# 3. How Git Stash Works

When you run:

```
git stash
```

Git will:

1. Save your **modified tracked files**
2. Reset your working directory to the **last commit**
3. Store the changes in a **stash stack**

So stash behaves like a **stack (LIFO)**.

Example stash list:

```
stash@{0}
stash@{1}
stash@{2}
```

The most recent stash is always **stash@{0}**.

---

# 4. Basic Git Stash Commands

## 4.1 Save Changes

```
git stash
```

This saves:

* modified tracked files
* staged changes

But **not untracked files**.

---

## 4.2 Save with Message

```
git stash push -m "Work in progress for login page"
```

Example output:

```
Saved working directory and index state WIP on main
```

This helps identify the stash later.

---

## 4.3 List Stashes

```
git stash list
```

Example output:

```
stash@{0}: WIP on main: Login page
stash@{1}: WIP on dev: Fix navbar bug
```

---

## 4.4 Apply Stash

Restore changes without removing the stash:

```
git stash apply
```

Or apply a specific stash:

```
git stash apply stash@{1}
```

---

## 4.5 Pop Stash

Apply changes **and remove the stash**.

```
git stash pop
```

Equivalent to:

```
git stash apply
git stash drop
```

---

## 4.6 Delete a Stash

```
git stash drop stash@{1}
```

---

## 4.7 Delete All Stashes

```
git stash clear
```

⚠️ This permanently deletes all stashed work.

---

# 5. Stashing Untracked Files

By default, stash ignores **untracked files**.

To include them:

```
git stash -u
```

or

```
git stash --include-untracked
```

---

# 6. Stashing Ignored Files

If you want to stash **ignored files** too:

```
git stash -a
```

---

# 7. Creating a Branch from a Stash

Sometimes the stash conflicts with the current branch.

Git allows creating a branch from the stash:

```
git stash branch new-feature stash@{0}
```

This will:

1. Create a new branch
2. Apply the stash
3. Remove it from stash list

---

# 8. Internal Structure of Git Stash

Internally, Git stores stash as **commits**.

Each stash contains:

1. Working directory changes
2. Staged changes
3. Reference to the original commit

You can inspect it:

```
git stash show
```

or detailed view:

```
git stash show -p
```

---

# 9. Example Workflow

### Step 1 – Modify files

```
index.html modified
style.css modified
```

### Step 2 – Save work

```
git stash
```

Working directory becomes clean.

---

### Step 3 – Switch branch

```
git checkout bug-fix
```

---

### Step 4 – Return to feature branch

```
git checkout feature-login
```

---

### Step 5 – Restore work

```
git stash pop
```

Your files return exactly as before.

---

# 10. Real Developer Use Cases

### 1 Fix urgent bugs

Save current work quickly.

```
git stash
```

Switch to bug branch.

---

### 2 Pull new changes safely

```
git stash
git pull
git stash pop
```

---

### 3 Experiment with code

Developers stash work before trying risky changes.

---

### 4 Temporary task switching

Example:

```
Feature A → stash
Work on Feature B
Return to Feature A
```

---

# 11. Advantages of Git Stash

✔ Keeps working directory clean
✔ Allows quick context switching
✔ Avoids unnecessary commits
✔ Supports multiple saved states

---

# 12. Limitations

❌ Can cause merge conflicts when applying stash
❌ Easy to forget stashed work
❌ Not suitable for long-term storage

---

# 13. Best Practices

### Use descriptive messages

```
git stash push -m "navbar responsive fix"
```

---

### Check stash list regularly

```
git stash list
```

---

### Do not keep stashes for long

They are **temporary storage**, not permanent history.

---

# 14. Git Stash vs Commit

| Feature            | Stash    | Commit   |
| ------------------ | -------- | -------- |
| Saved in history   | ❌        | ✔        |
| Temporary          | ✔        | ❌        |
| Requires message   | optional | required |
| Shared with others | ❌        | ✔        |

---

# 15. Summary

**Git Stash** is a powerful feature in **Git** that allows developers to **temporarily store unfinished work** without committing it. It helps developers **switch tasks quickly**, keep repositories clean, and manage incomplete changes efficiently.

---

If you want, I can also show you:

* **Advanced Git Stash commands used by senior developers**
* **Common Git Stash interview questions**
* **Visual workflow of Git Stash**
* **Hidden Git Stash tricks used in large teams**

Just tell me.
