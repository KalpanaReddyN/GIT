## git reset:
-------------
    git reset moves the current branch pointer (HEAD) to a different commit — essentially "erasing" commits from the history. It has 3 modes:

    1. git reset --soft <commit>
        Moves HEAD to <commit>, keeps staged and working directory intact. Your changes stay in the staging area
            git reset --soft HEAD~1

    2. git reset --mixed <commit> (default)
        Moves HEAD and unstages files. Changes stay in your working directory
        git reset HEAD~1

    3. git reset --hard <commit>
        Moves HEAD and wipes out all changes. DANGEROUS — deletes commit history and local changes!
            git reset --hard HEAD~1

    ⚠️ Use reset only on local/private branches — never on shared or public branches, as it rewrites history.

## git revert:
-------------
    git revert creates a new commit that undoes the changes made by a previous commit — without rewriting history.
        git revert <commit>
    Safe for shared branches. Used when you want to undo a commit but keep the commit history intact. Helpful in production environments where history integrity is critical

    🧠 Example Use Cases
        Use **reset** if:
            You're working alone and want to remove or redo local commits
            You made a mistake and want to "go back in time"
        Use **revert** if:
            You're working on a shared branch (like main)
            You need to undo a bad commit without affecting others' history

