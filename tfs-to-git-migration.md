## Purpose
This document is to help migrate source code from TFS to Git with all historical changesets and branches.

## Steps
1. Install **Chocolatey**, using [this instruction](https://chocolatey.org/install). 
   * If you want to know "What is **Chocolatey**?", go [here](https://chocolatey.org/). 
   * *Note*: you can choose not to use **Chocolatey** but it makes thing harder when you have to search for correct installation to download or also setup all other stuffs like **PATH** in **System Environment**, etc.
2. Open **Command Prompt** or **Power Shell** in Administrator Mode
3. Install **git-tfs** ```choco install gittfs```
4. Create separate folder for git repo since it can mess up your current code
5. Go to folder on step 4 and run ```git tfs clone [tfs team collection] [project branch] . --branches=all```
   * Here is the sample command to clone iSearch source code from TFS to local git repo ```git tfs clone http://[tfs server]:8080/tfs/[collection] $/[project]/[branch] . --branches=all```
   * You should check branch hierarchy and select root branch to clone. For example: Main on above command.
   * Use ```--branches=all``` parameter when you want to maintain the same structure as TFS has. I would recommend this because it creates branches as same as TFS.
5. Add [.gitignore](.gitignore) and [.gitattributes](.gitattributes) files to avoid headache with both Windows and Linux
6. Create repo on Git Enterprise and copy git URL
6. Add remote URL to local git repo ```git remote add origin [git URL]```
7. Push all branches to remote repo ```git push --all```
