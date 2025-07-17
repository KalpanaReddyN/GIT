## How to push our existing folder in vs code to github

    1) Open the folder path in vs code and type git init on terminal.
    2) . git folder will be created
    3) Create a folder in git with same name as the folder in vs code.
    4) git remote add origin <link>    ## this comes from the above created git repo on the bottom right side.
    5) git branch -M main     ## Now the branch is converted to main
    6) git add .
    7) git commit -m "write the commit message here"
    8) git push -u origin main


## How to get the already existing git repo to my vscode

    1) git clone <repository-url>
    2) cd repository
    3) git pull origin main
    4) The new repo will be seen in our vs code and make changes and push the code to github using below commands
    5) git add . ; git commit -m "message" ; git push origin main
    



