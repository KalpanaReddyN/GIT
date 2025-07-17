## Git Has 3 Main Areas:
    Working Directory
        Where you edit files (e.g., in VS Code).

    Staging Area (Index)
        Where you prepare files to be committed using git add.

    Commit Area (Repository History)
        Where Git stores your committed snapshots after git commit.

## git reset:
-------------
        Git reset is used when I need to undo commits or adjust the commit history. It allows you to move the HEAD pointer and either modify the staging area or the working directory depending on the reset type (soft, mixed, or hard). 
        For example, if I accidentally committed the wrong changes, I can use git reset --soft HEAD~1 to uncommit the changes but keep them staged, or git reset --hard HEAD~1 to completely discard them.
            
    1. git reset --soft <commit>
        Moves HEAD to <commit>, keeps staged and working directory intact. Your changes stay in the staging area and removed from commit area. 
            git reset --soft HEAD~1

    2. git reset --mixed <commit> (default)
        Moves HEAD and unstages files. Changes stay in your working directory. it will remove the changes from staging area, commit area and keep the code in workspace.
        git reset HEAD~1

    3. git reset --hard <commit>
        Moves HEAD and wipes out all changes. changes will be removed from commit, staging and workspace. DANGEROUS — deletes commit history and local changes!
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

## Restore  

        Restore works on particular file, reset or revert works on entire workspace..
        If you've made changes to a file and want to revert it to its last committed state, you can use git restore. 
        If you've added files to the staging area using git add but want to unstage them, git restore allows you to easily do that.
        
        git restore <file>
            • --source=<commit>: Specify which commit to restore from (default is HEAD).
            • --staged: Unstage a file, i.e., move it from the staging area back to the working directory.
            • --worktree: Restore files in the working directory to their last committed state.
            
        Ex: you may accidentally modify configuration files and want to revert them to their original state without affecting the commit history. You were working on a Kubernetes configuration file (k8s-deployment.yml), and you want to revert it back to the state it was in at the last commit because you realized the change was incorrect. git restore k8s-deployment.yml This will discard your changes to that file and restore it to the last committed state.

        EX: You stage some files using git add, but then realize that they are not ready to be committed. You can easily unstage them using git restore --staged, which is much clearer than using git reset.
        You staged app.py for a commit but realized it's not ready yet, so you unstage it: git restore --staged app.py This removes it from the staging area but keeps any local changes you made.
        
        EX: where a previous commit had a more stable configuration or code and needs to restore that version, perhaps to fix a configuration bug.
        You want to restore a configuration file to its state in a previous commit because the latest changes were problematic. git restore --source=abc1234 config.json This restores the config.json file to the state it was in at commit abc1234.

## Cherry pick 

        When you find something useful in another branches, you can pick those commits instead of completely merge or rebase with that branch.
            git cherry-pick <commit-id>
        
        EX:
        Imagine 2 features branches, feature-1 and feature-2. 
        feature-2 finds something useful in feature-1 instead of completely merging with it we can cherry pick the commits we want.
            git checkout feature-1
            git pull
            git checkout feature-2
            git log feature-1 --> you can see the commits, select what you want
            git cherry-pick <commit-id> --> this may create conflicts, resolve and push
        
        • Git cherry-pick is a command used when I want to selectively apply specific commits from one branch to another without merging the entire branch. For example, if a bug fix was made in a feature branch and I want that fix in main, I can cherry-pick just that commit, which applies the changes to main. The commit will be added as a new commit to the branch I’m working on, which keeps the history clean without merging other unrelated changes.
        • It's particularly useful for applying hotfixes, backporting changes, or when I want to grab specific commits from a branch, like when working on a production branch and needing just one change from a feature branch.

