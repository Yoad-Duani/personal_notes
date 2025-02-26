# Understanding Git Stash

## Simple git stash

**Explanation**

- **`git stash`**: Temporarily saves your changes without committing them.
- **`git stash pop`**: Applies the stash and removes it from the stash list.
- **`git stash apply`**: Applies the stash but keeps it in the stash list.

**Commands**

```bash
git stash          # Save changes to the stash
# Make sure your working directory is clean before popping or applying

git stash pop      # Apply the stash and remove it
# OR
git stash apply    # Apply the stash but keep it in the stash list
```


---

## Working with Multiple Stashes

**Explanation**

- **`git stash list`**: View all saved stashes.
- **Named Stash**: Add a name for easy identification.
- **Apply Specific Stash**: Use the stash name or ID.

**Commands**

```bash
git stash push -m "Feature work"                        # Stash named stash

git stash push -m "Feature work" --include-untracked    # Stash untracked files

git stash push -m "Feature work" -S                     # Stash staged files

git stash list                                          # List all stashes

# Apply a specific stash
git stash apply stash@{1}                               # Apply stash by ID

git stash pop stash@{1}                                 # Apply and remove stash by ID

# Apply a specific stash by name
git stash apply "stash^{/Feature work}"                 # Apply stash by name

```

## Resolving Conflicts with Stash

**Explanation**

- Sometimes applying or popping a stash can lead to conflicts if the working directory has changes that conflict with the stashed changes.
- Git will notify you of the conflict, and you must manually resolve it.

**Commands**
```bash
git stash pop                        # Attempt to pop the stash
# If there are conflicts, Git will notify you

# Resolve the conflicts manually using your editor or Git tools

# After resolving the conflicts

git add <file>                       # Stage the resolved files

git stash drop                       # Drop the stash if it was successfully applied
```

---

## Remove stash

**Explanation**

- **`git stash drop`**: Remove a specific stash.
- **`git stash clear`**: Remove all stashes.

**Commands**
```bash
git stash drop stash@{1}            # Drop a specific stash

git stash clear                     # Clear all stashes
```

<br />

## Full Example
