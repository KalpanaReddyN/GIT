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

    When you run __git log__ in a Git repository, it displays a history of all commits made in the current branch by default.
    


