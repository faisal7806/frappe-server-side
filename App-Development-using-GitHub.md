##Basic Development Commands
###Forking Frappe / ERPNext
In order to make changes to Frappe and ERPNext, you need to set up a fork on your own GitHub account. This can be done easily on the GitHub website.

1. Log in to GitHub
2. Go to github.com/frappe/frappe
3. Click on the Fork button at the top right of the screen.
4. Follow the instructions.

###Setting up local access to your fork
When making changes to your local installation, you will need to be able to update the online repository so that you can push changes to Frappe / ERPNext, as well as keep revisions on GitHub, etc.

1. Access your local installation using a terminal and go to the `frappe-bench` folder
2. For each app you have forked, use the following commands to establish a remote to your fork:

    ```
    cd apps/[app_name]
    git remote add origin https://github.com/[username]/[app_name]
    ```

3. Use the following command (in each apps/app_name folder) to verify the remote has been added

    ```
    git remote -v
    ```

###Pulling the latest data from your fork
Typically, using bench update will pull the lastest data from the upstream (github.com/frappe) server, if pulling frappe or erpnext. If you want to pull your own fork from the repositories, you can use the following command, from the apps/[app_name] folder.

```
git pull origin [branch_name]
```

###Starting to write your own code
When you start making changes, whether to frappe/erpnext, or to modify your own app, you need to track those changes within a new branch. This allows your to push just these changes to your own github repository, which will allow you to create pull requests and merge the branch into the frappe/erpnext code, or your own app. The full procedure for starting changes all the way to pushing to your online repository is described below.

1. Go to your app/[app_name] folder on your local server (through a terminal)
2. Create a new local branch:

    ```
    git checkout -b [my_branch_name]
    ```

3. Make changes to your app. This can be done either in the code of your app, or using the web interface of frappe to edit/add doctypes, etc. 
4. When finished making changes, go back to the terminal in your app/[app_name] folder and find out which files have been modified:

    ```
    git status
    ```

5. A list of files, each highlighted red will appear. If you want to include the changes to those files in your commit, add them using:

    ```
    git add [file_name]
    ```
    If you want to add all the files that were changed, use:
    ```
    git add  .
    ```

6. Commit the changes to the branch

    ```
    git commit -m "[message]"
    ```

    where the message is a short description of the changes you made in this commit

7. Push the changes from this commit to your repository

    ```
    git push origin [branch_name]
    ```

8. If you are done making changes to this branch, change back to the master or develop branch (depending on what were on before)

    ```
    git checkout master
    ```

###Creating a pull request
Once you have a branch that has some useful contribution that you want to make part of your main branch, you can create a pull request for that branch and merge the changes.

1. Go to your repository through a web browser (https://github.com/[user_name]/[repository]
2. Click the New Pull Request button
3. Select the base fork to the repository you want to merge into, the base branch to the branch you want to merge into, the head fork to your repository and the compare branch to the branch with your changes.
4. Review the changes and make sure that they match the changes you wanted to make.
5. If you are happy with the changes, click the create pull request button.

###Bringing your repository in line with the upstream repository
Because of the high level of development that occurs within Frappe and ERPNext, you will find that very quickly your forked repository goes out of date with the upstream one. 

1. Go to the apps/[app_name] folder in your terminal
2. Make sure you are checked out on the branch you want to fix (master or develop typically)

    ```
    git checkout [branch_name]
    ```

3. Pull the latest data from the upstream repository

    ```
    git pull upstream [branch_name]
    ```

4. Rebase your local version to the correct repository/branch

    ```
    git rebase upstream/[branch_name]
    ```

5. Check to see if everything went well

    ```
    git status
    ```

6. Force your forked repository to use your rebased local data

    ```
    git push origin [branch_name] --force
    ```

###Testing a branch
Often times, you might find that you want to try out a branch from another developer:

1. Add the repository as a remote

    ```
    git remote add [repo_name] http://github.com/[repo_link]
    ```

2. Pull the latest from the repository

    ```
    git pull [repo_name]
    ```

3. Check out the branch from the repository

    ```
    git checkout [branch_name]
    ```

4. Migrate the bench to take hold of the changes. In the `frappe-bench` folder:

    ```
    bench migrate
    ```
