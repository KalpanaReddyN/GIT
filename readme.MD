### How to push our existing folder in vs code to github

    1) Open the folder path in vs code and type git init on terminal.
    2) . git folder will be created
    3) Create a folder in git with same name as the folder in vs code.
    4) git remote add origin <link>    ## this comes from the above created git repo on the bottom right side.
    5) git branch -M main     ## Now the branch is converted to main
    6) git add .
    7) git commit -m "write the commit message here"
    8) git push -u origin main


### How to get the already existing git repo to my vscode

    1) git clone <repository-url>
    2) cd repository
    3) git pull origin main
    4) The new repo will be seen in our vs code and make changes and push the code to github using below commands
    5) git add . ; git commit -m "message" ; git push origin main
    
### Branching

    1) By default, Git has a branch called main or master, depending on the repository setup. New branches allow you to work on different tasks simultaneously without interfering with the main project. Making changes directly in the main branch is risky because it often represents production-ready code. Therefore, it's always best practice to create a feature branch for any new work. Each branch represents a different scope of work, allowing team members to work independently and merge their changes later. This also enables testing new ideas without affecting the stable code.

    2) To maintain code quality and stability, it's important to enforce pull requests before merging into the main branch. This can be configured in GitHub by navigating to Settings → Rules → Rulesets, selecting or creating a ruleset for the main branch, setting the Enforcement Status to Active, and enabling “Require a pull request before merging.” This ensures all changes are reviewed and tested before being included in production.
    
    3) After creating a new feature branch (e.g., feature/eks-setup) and push the changes to GitHub. A pull request (PR) is then raised to merge the branch into the main branch. 
    
    4) Once the PR is submitted, automated checks often run as part of a continuous integration (CI) pipeline. These checks may include code formatting, validation, testing, and security scans to ensure the changes are correct and safe. Team members or leads review the pull request, provide feedback if needed, and approve it once everything looks good. 
    
    5) After approval and successful checks, the PR is merged into the main branch. In some workflows, this merge may trigger further automated steps such as deployments or releases. This structured process ensures that all changes are reviewed, tested, and traceable before becoming part of the main project.

    Workflow:  
            ○ Create a Branch: Start a new branch for a feature or fix.
            ○ Switch Branches: Move between different branches to work on specific tasks.
            ○ Merge Branches: Combine changes from one branch into another.
            ○ Delete Branches: Clean up branches that are no longer needed.
    
## SHA Code
    
    SHA stands for Secure Hash Algorithm, and in Git, it refers to the unique identifier (a commit hash) that Git assigns to every commit you make.
    EX: 40-character string looks like ---> 6e559cb8c1a3e909d2a9b19360cf8324b0f7a46c

    • Each commit is assigned a unique SHA code. This ensures that no two commits in the same repository can have the same identifier, even if the changes are identical.
    • SHA codes are used to reference specific commits in the repository's history. This is useful for viewing changes (git show <SHA>), reverting to an earlier state, or merging changes
    • It ensures the security and accuracy of the version control system.

    When you run git log in a Git repository, it displays a history of all commits made in the current branch by default.
    

## Two different ways to integrate changes from one branch into another
    1)  merge
            A merge commit has two parent commits — it’s created when one branch is merged into another. Merging preserves the complete commit history, which means at any point, you can track all changes, who made them, and how branches evolved. Git does not rewrite past commits, making this approach transparent and safe for collaborative workflows.

            When a pull request (PR) is approved, someone (usually the author or a maintainer) clicks "Merge", and Git creates a new merge commit with a unique ID. This commit represents the point where two branches were combined.

            Merge commits are very useful for debugging, as they clearly show when and what features or fixes were integrated. If something breaks after a merge, it's easier to trace the problem by checking the merge commit.

            Merging also allows teams to work independently on different branches and later integrate their changes into the main branch without losing context or overwriting each other's work. It supports a safe, organized workflow in collaborative environments.
            
    2) rebase 
            Rebase is a Git operation that moves or reapplies your branch's commits onto another base branch — typically to make the commit history linear and clean. Instead of preserving the branching structure like merge, rebase rewrites history by creating new commits that appear as if they were created on top of the target branch all along.

            When you run git rebase main on a feature branch, Git temporarily removes your feature branch's commits, applies the latest commits from main, and then re-applies your work on top — as new commits. This makes the project history appear as if everyone worked in a straight line, which can be easier to read and review.

            Rebase is especially helpful for keeping a clean, readable commit history, free from unnecessary merge commits. It’s commonly used before opening a pull request, to ensure that your branch is up-to-date with the latest changes in main.

            However, because rebase rewrites commit history, it should only be used on local or private branches — never on shared branches that others are working on. Rebasing shared branches can cause confusion and conflicts for your teammates.

            Rebase is a powerful tool when used carefully. It’s ideal for polishing your branch's history before merging, making the project history easier to maintain and understand in the long term.        

## Merge Conflict

    A merge conflict occurs when Git is unable to automatically merge two branches because they contain conflicting changes in the same part of a file. This usually happens when multiple team members modify the same lines of code or structure files differently in separate branches. When you attempt to merge, Git pauses the process and highlights the conflicting files. These files will contain special conflict markers (<<<<<<<, =======, and >>>>>>>) showing the differences between the two versions. As a developer, you must manually open each conflicted file, decide which version to keep (or combine both), and edit the file accordingly. Once the conflicts are resolved, you stage the changes using git add and complete the merge with a git commit. Merge conflicts are a normal part of collaborative development, and resolving them carefully ensures that no work is lost and the project remains stable. Regularly syncing your branch with the main branch and coordinating with your team can help minimize the frequency of conflicts.

## Branching Strategies
    1) Git Flow
        Git Flow is a Git branching model that organizes work around well-defined branch types to support structured development, releases, and hotfixes. It helps teams manage features, track production-ready code, and handle emergency fixes in a clean, collaborative way.
        
        Core Branches in Git Flow:
            main (or master):
                This branch holds production-ready code. All releases are tagged and deployed from here.
            develop:
                Contains the latest in-progress code that will go into the next release. New features are merged into this branch.
        
        Supporting Branches
            Feature Branches (feature/xyz):
                Created from: develop
                Used for: Adding new features
                Merged back into: develop
                Example: feature/user-authentication

            Release Branches (release/x.y.z):
                Created from: develop
                Used for: Final testing, bug fixing, preparing a release
                Merged into: both main and develop
                Example: release/1.0.0

            Hotfix Branches (hotfix/bug-id):
                Created from: main
                Used for: Critical fixes in production
                Merged into: both main and develop
                Example: hotfix/login-crash
        
        Git Flow Lifecycle (Typical Process):
            Start with a stable main and a working develop branch.
            Developers create feature branches from develop and work independently.
            Once features are complete, they are merged into develop.
            When it's time for a release, a release branch is created from develop. Final QA, minor fixes, and prep (like version bumps) happen here.
            The release branch is then merged into main (for deployment) and also back into develop (to keep develop updated).
            If an urgent bug occurs in production, a hotfix branch is created from main, patched, and merged back into both main and develop.
        
        Benefits of Git Flow
            Clear separation of production, development, and features
            Easy to manage hotfixes and urgent patches
            Ideal for teams with defined release cycles
            Promotes parallel development without interfering with stable code

    2) Feature Branching Model
        The Feature Branching Model is a Git workflow where every new feature, bugfix, or task is developed in a dedicated branch, separate from the main production code. This model helps keep development organized, isolated, and collaborative — without affecting the stable code in the main branch.

        Key Concepts:
            main or master Branch:
                Contains production-ready, stable code.Never develop directly on main.

            Feature Branches (feature/xyz)
                Created from: main (or sometimes develop in Git Flow setups)
                Used for: Working on individual features or tasks
                Merged back into: main via a Pull Request (PR)

            Naming examples:
            feature/login-page
            feature/add-user-role
            bugfix/reset-password
            hotfix/crash-on-startup
        
        Typical Workflow:
            ✅ Start on main:
                    git checkout main
                    git pull origin main
            🌿 Create a new branch:
                    git checkout -b feature/user-registration
            💻 Make your changes and commit:
                    git add .
                    git commit -m "Add user registration form"
            🚀 Push your feature branch:
                    git push origin feature/user-registration
            🔁 Create a Pull Request (PR) on GitHub/GitLab/Bitbucket
                    Review happens here. Once approved, merge to main
            🧹 Optionally delete the feature branch after merging:
                    git branch -d feature/user-registration

        Advantages of Feature Branching:
            Isolation: Developers work independently without affecting others
            Safe collaboration: Changes aren’t merged until reviewed and approved
            Clean history: Easy to trace features or bugs through branch names and commits
            Better CI/CD: Code can be automatically tested in feature branches before merging