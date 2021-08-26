# Setting up your development environment

## Installing node and npm

### What is node?

Node.js is an open-source, cross-platform, back-end JavaScript runtime environment that runs on the V8 engine and executes JavaScript code outside a web browser. Node.js lets developers use JavaScript to write command line tools and for server-side scripting—running scripts server-side to produce dynamic web page content before the page is sent to the user's web browser. Consequently, Node.js represents a "JavaScript everywhere" paradigm, unifying web-application development around a single programming language, rather than different languages for server-side and client-side scripts.

### What is npm?

npm is two things: first and foremost, it is an online repository for the publishing of open-source Node.js projects; second, it is a command-line utility for interacting with said repository that aids in package installation, version management, and dependency management. A plethora of Node.js libraries and applications are published on npm, and many more are added every day. These applications can be searched for on [https://www.npmjs.com/](https://www.npmjs.com/). Once you have a package you want to install, it can be installed with a single command-line command.

### Installation

Download the "LTS" version of node (not "Current") and go through the installation process: [https://nodejs.org/en/download/](https://nodejs.org/en/download/)

### Confirming node and npm have been installed successfully

1. Open a new terminal window
2. Run the command `node -v`
3. You should see it output a version number of at least `v14.16.1`
4. Run the command `npm -v`
5. You should see it output a version number of at least `6.14.12`

## Installing and configuring git and Github

### What is git?

Git is a free and open source distributed version control system designed to handle everything from small to very large projects with speed and efficiency.

### What is Github?

GitHub is a website and cloud-based service that helps developers store and manage their code, as well as track and control changes to their code.

### Installation

Installing on macOS

1. In a terminal window run the command `git --version`
2. If you already have git installed it should output the version number
3. If you do not have git installed, it should prompt you to install it

Installing on Windows

1. Follow the steps in the following link: [https://zarkom.net/blogs/how-to-install-git-and-git-bash-on-windows-9140](https://zarkom.net/blogs/how-to-install-git-and-git-bash-on-windows-9140)

After installation, open your terminal and run the following commands replacing the name and email with your own

1. `git config --global user.name "Your Name"`
2. `git config --global user.email "your@email.com"` (ensure your email is the same as your github account)

Git tutorial: [https://www.notion.so/Introduction-to-Git-ac396a0697704709a12b6a0e545db049](https://www.notion.so/Introduction-to-Git-ac396a0697704709a12b6a0e545db049)

### Confirming git has been successfully installed

1. In a terminal window run the command `git --version`
2. You should see it output a version number of at least `git version 2.28.0`

## Installing Firebase

### What is Firebase?

Firebase is a platform developed by Google for creating the backend for mobile and web applications through offering various services and tools including but not limited to user authentication, NoSQL database and file storage. Firebase also provides tools for tracking analytics, reporting and fixing app crashes, creating marketing and product experiment.

### Installation

1. In a terminal window run the command `npm install -g firebase-tools`
2. Then, login to your google account by running the command `firebase login`

### Confirming Firebase has been successfully installed

1. In a terminal window run the command `firebase --version`
2. You should see it output a version number of at least `9.2.1`

## Installing VSCode

### What is VSCode?

Visual Studio Code is a code editor redefined and optimized for building and debugging modern web and cloud applications.

### Installation

1. Download VSCode for your respective platform from the link [https://code.visualstudio.com/download](https://code.visualstudio.com/download)
2. For mac: Drag the installed VSCode application to the applications folder
3. For windows: Go through the installation process

## Installing ESLint and Prettier

### What is ESLint?

A pluggable and configurable linter tool for identifying and reporting on patterns in JavaScript used for catching bugs and maintaining code quality.

### What is Prettier?

Prettier is an opinionated code formatter. It enforces a consistent style by parsing your code and re-printing it with its own rules that take the maximum line length into account, wrapping code when necessary

### Installation

1. Open VSCode
2. Click on the extensions icon on the left panel (looks like four squares with a displaced top-right square)

<img width="87" alt="Screen Shot 2021-08-26 at 4 19 30 PM" src="https://user-images.githubusercontent.com/35095726/131030780-f2de1085-0d1d-4ad7-81f7-2c6a1d262ffb.png">

4. Search for the extension "ESLint" and install the first extension (the author should be "Dirk Baeumer")

<img width="696" alt="Screen Shot 2021-08-26 at 4 19 38 PM" src="https://user-images.githubusercontent.com/35095726/131030809-912ce144-4d6f-4193-ba8c-c1a2a707037f.png">

6. Search for the extension "Prettier - Code formatter" and install the first extension (the author should be "Prettier")

<img width="692" alt="Screen Shot 2021-08-26 at 4 19 46 PM" src="https://user-images.githubusercontent.com/35095726/131030834-7ada61bd-6700-47f1-addb-fd9d21d2031c.png">


8. Open your VSCode settings and type format in the searchbar
9. Change the following settings
   1. Editor: Default Formatter => "Prettier - Code formatter"
   2. Editor: Format On Paste => check the checkbox
   3. Editor: Format On Save Mode => "file"
10. Ensure your settings match with the image below

<img width="917" alt="Screen Shot 2021-08-26 at 4 19 19 PM" src="https://user-images.githubusercontent.com/35095726/131030909-3e90eae9-9f57-4712-a7ee-96ec665522ef.png">

### Confirming ESLint and Prettier have been successfully installed

1. Create a new folder on your desktop
2. Open the folder in VSCode
3. Open a new terminal window using control + \` or through `View > Terminal`
4. Run the command `npm init -y` to initialize a new node project
5. Running this command should automatically create a new file called package.json
6. Create a new file called `.prettierrc`
7. Simply add a pair of curly brackets {} on the first line of the file and save the file
8. Create a new file called index.js, copy the following code, and paste it into the file

```js
function hello    () {




 console.log(     "hello world"))
}
```

9. When you save the file, you should see a red line appear under the second closing bracket in the `console.log` statement like in the image below

<img width="429" alt="Screen Shot 2021-08-26 at 4 19 59 PM" src="https://user-images.githubusercontent.com/35095726/131030972-0917483d-8abf-4437-80b5-06694ff014ea.png">

10. If the red line appears in your file, it means ESLint was installed successfully
11. Now go ahead and delete the extra bracket at the end of the `console.log`
12. The red line should disappear once you delete the extra bracket
13. Now save the file and the code should magically format like in the image below

<img width="424" alt="Screen Shot 2021-08-26 at 4 20 05 PM" src="https://user-images.githubusercontent.com/35095726/131031004-1dd60ae0-f12a-40fb-a300-98c452ed78f8.png">

14. If this code automatically formats, it means Prettier was installed successfully


## Working on a StudyFind project

1. Ensure your Github account is invited to the StudyFind organization
2. Ensure you have write access to the repository you want to work on (contact Yohan if you do not)
3. Open your terminal and use the command `cd <directory_path>` to navigate to the directory you want to clone your project in
4. You can confirm you are in the appropriate directory by printing out its path using the command `pwd`
5. Now copy the HTTPS URL of the github repository you want to clone (see image below)

<img width="392" alt="Screen Shot 2021-08-26 at 3 06 19 PM" src="https://user-images.githubusercontent.com/35095726/131031110-00f2e766-a02a-480b-bc01-fc55a4e81ad6.png">

7. Run the command `git clone <repository_url>` where the `repository_url` is the URL you copied in the previous step
8. Wait for github to clone the repository in the directory
9. If you are facing any issues with cloning, it's likely that your git has not been configured properly or there may be missing permissions
10. Now navigate into the cloned repository using `cd <repository_name>`
11. HINT: To see the names of all files and folders in the directory use the command `ls`

For React Projects

1. Run the command `npm install` and wait for all the node dependencies to finish installing
2. Run the command `npm start` to start the project which will automatically open in the browser at [http://localhost:3000](http://localhost:3000)
