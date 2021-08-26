# Using Github

*Author: Keely Culbertson*

I’m trying to keep this general because I use a Mac and I’m not sure exactly where it differs from
Windows

**To create a repository:**

1. You can create a repository on Github (easiest I think) and clone it onto your computer,
or you can use Git
2. To use Git, navigate to the folder that you want to hold the repository using terminal or
command line
3. Use the command “git init” to initialize the repository for this folder

**To add a repository that was created on the website to you computer:**

1. Copy the clone link from the GitHub website
2. Create a folder on your computer that will hold the repository
3. In your terminal or command prompt, navigate to the folder you want to hold the
repository
4. Use the command “git clone” and paste the link after the clone (with a space between
clone and the link)

**To get changes from your repository:**

1. In your terminal or command prompt, navigate to the folder that holds the repository
2. You can use the command “git fetch” to see if there are changes to the repository
3. Use “git pull” to pull the changes from Github to your computer

**To save changes:**

1. In your terminal or command prompt, navigate to the folder that holds the repository
2. Use the command “git add .” to add all of your changes with Git
3. Use the command “git commit -m “”” and in the quotes, put a message that will be the
title of your push
4. Use the command “git push” to push all the changes to Github

**To create a branch:**

1. You can create a branch on the Github website or through git
2. In your terminal or command prompt, navigate to the folder that holds the repository
3. Use the command “git branch name” and replace the word name with what you want to
name the branch

**To switch branches:**

1. In your terminal or command prompt, navigate to the folder that holds the repository
2. Use the command “git checkout branch” and replace the word branch with the name of
the branch you want to switch to

**To merge branches:**

1. You can merge branches on the Github website or through git (it might be better to do it
through the website because, if there are conflicts between the branches, you can better
choose what changes to keep or discard)
2. In your terminal or command prompt, navigate to the folder that holds the repository
3. Checkout the branch that contains the changes you want to merge to another branch
4. Use the command “git merge branch” and replace the word branch with the branch that
you want all the changes to be added to

**Other commands:**

* “git status” in your repository to see the changes you’ve made that haven’t been
committed yet
* “git stash” in your branch to save changes you don’t want to commit yet but want to pull
new changes