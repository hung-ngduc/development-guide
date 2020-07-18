## Setup Windows Machine
1. Install **Chocolatey**, using [this instruction](https://chocolatey.org/install). 
   - If you want to know "What is **Chocolatey**?", go [here](https://chocolatey.org/). 
   - *Note*: you can choose not to use **Chocolatey** but it makes thing harder when you have to search for correct installation to download or also setup all other stuffs like **PATH** in **System Environment**, etc.
2. Open **Command Prompt** or **Power Shell** in Administrator Mode
3. Install NodeJS: ```choco install nodejs```
4. Install Yarn: ```choco install yarn```
5. Setup EOG npm server, follow [this instruction](https://git.eogresources.com/web-technologies/guides/blob/master/package_management/npm/publish-private-package.md)

## Chocolatey
**Chocolatey**, similar to **HomeBrew** on Mac, is powerful tool on Windows which not just help you install all things related to react with no hassle, but also help you install all other available software like: ```docker```, ```rabbitmq```, etc or utility like ```notepad++```.

### Useful Chocolatey Commands
- ```choco list```: to list out all existing packages on internet
- ```choco list node```: to list out all packages having *node* in name
- ```choco install [package name]```: to install package
- ```choco uninstall [ package name]```: to uninstall package
- ```choco upgrate [package name]```: to upgrade package

## Create React App
You can find below instruction online but I just put it here for your convenience. Open Command Prompt and type or copy/paste below commands to get started on **React**.
1. ```npm install create-react-app```
2. ```npx create-react-app [app name]```
3. ```cd [app name]```
4. ```npm install```
5. ```npm start``` or ```yarn start```

## Visual Studio Code
I use [Visual Studio Code](https://code.visualstudio.com/) to work with React app, but there are several tools out there for this purpose, you can choose the best one works for you.
