# What to Expect

This file summarizes the git commands we talked about on the 4th FCA Bootcamp session (10/07/2024). Each command is sectioned off by an h1 title (like the "What to Expect" above), so if there is a command that interests you then you can use quickly jump to it. Additionally, with each command you'll find subsections of simple errors with possible causes in case you ever need to troubleshoot. 

Here are some quick housekeeping notes before we begin. We will be reviewing all the commands as Terminal/Command Prompt commands, but if you wish to follow along via a GUI tool like Github Desktop feel free. We recommend following along with the git CLI (Command Line Interface), though, since knowing how to navigate that environment is an equally valuable skill. Additionally, this document is "opinionated", meaning that we will discuss commands alongside certain good practices. What this means for you is that this is not the *only* way to use these git commands, but following these practices will guarantee that you don't run into any troublesome issues during your git journey. With that said, happy reading!

# Install `git`

Before we can begin using git, we need to make sure we actually have it. Even if you don't remember installing git yourself, there is a chance it's already on your device for some reason or another. To check if you have it installed, open Terminal/Command Prompt and enter the following command.

```
git -v 
```

If you have git installed already, you should see some kind of non-error response containing your git version. The rest of this section is installing git, so if you already have git installed then you can skip straight to the next section. 

To install git, either look up "git download" or use [this link](https://git-scm.com/downloads). Select your platform and follow the relevant instructions. This step should be pretty straight-forward, but if you encounter any issues then feel free to reach out to us or google the issue.

After installing git, close your current Terminal/Command Prompt window. Open a new window and try running the above command again to verify if the install worked.

# Make a Github Account

Github is a service that makes use of git to manage git repositories. There are many such services, but Github is the easiest to get started with due to its popularity.

Visit the [Github Website](https://github.com/) to get started. If you don't have an account already, you can make one here. We recommend using your PSU email for a generally smoother process, but you are free to use your personal email if you wish.

Once you make your account, feel free to make a test repository by clicking the green "new" button in the left column of your Github home screen to use the below commands on!

# Make a Git Repository

Now that we have a place on Github for our repository, let's actually make it. This can be done in a few different ways, but the way we'll be using here is to create a local git repository locally and then linking it with the repository namespace on Github. Navigate to wherever you want to save your project and make a folder for the project. If you don't have it open already, make a new Terminal/Command Prompt session and navigate to wherever you made this folder. While this is not a Terminal/Command Prompt tutorial, below are some simple commands to help anyone who might need them. If you have any specific questions, you're free to contact us as always!
- `cd <Directory Path>`
	- Allows you to Change your Directory/Folder to whichever path you specified. Supports both absolute paths and relative paths. To go one level up the path tree (go from `Desktop/Photos/Thanksgiving2023` to `Desktop/Photos`, for example), you can use `cd ..` to do so. 
- `ls <Directory Path>`
	- Lists all files/folders in your current directory. If no path is given, it will print your current directory's contents out by default.
	- For windows `dir` does something similar.
- `mkdir <Directory Name>`
	- Makes a new directory/folder in your current directory. 

Once you've successfully navigated to your folder, run the following command.

```
git init
```

This will turn this folder into a git repository. This works on any folder, whether it is empty or not. You'll know if the git repository was successfully initialized by whether there is a `.git` folder. 
- Just as a side note, don't create a Git Repository within a Git Repository. That is, before running the `git init` command, check if your folder exists inside an already existing git repository before doing so.

# Connect to Github

The next step is to link our local repository with our empty repository on Github. Before we do this, though, let's put something in our local repository to know that it all works.

While git is primarily used in coding applications, it can be used for anything. Git is a technology designed to reconcile changes made by multiple people in a repository. Thus, to keep things simple, let's create a text file. You're free to make whatever you want (Python, Java, C++, etc), but a text file works just fine. 

Once you make your text file and write whatever you want, it's time to actually connect to Github for the first time. Navigate to the empty repository on Github and copy the link that should be present. Make sure you're on the `HTTPS` option and not the `SSH` option. Once you copy this link, navigate to the terminal and type the following command.

```
git remote add <remote_name> <remote_link>
// A common remote name is "origin", so your command might look something like
git remote add origin https://github.com/NickFalletta29/FCA_bootcamp.git
```

You can verify if you successfully added the remote by using the following command.

```
git remote -v
```

If you see 2 links (fetch and push), then you've successfully added your remote. 

You can think of a remote in git as git's way of saving your repository's location. Now anytime you see `origin` (or whatever you named your repository), both you and git know what it points to.

# Add, Commit, Push

`add`, `commit`, and `push` are the "trinity" of git commands. Let's break them down as we use them!

```
git add -A
// or
git add .
// or
git add *
```

The first step is to "select" all the documents we want git to work with. In most cases, you should just add every file in your project by using one of the above command arguments. If for some reason you want to only select a certain file(s), you can just provide the link instead. If you have a lot of files that you don't want pushed (like `node_modules` in a JS project), then you can specify what kinds of files you don't want in a `.gitignore` file. 

Anyway, by running the `add` command, git is now selecting everything in our local repository. The next step is to tell git to write a "commit log" of all the activity that's occurred since the last time we made a commit log. 

Commit logs are also something you can expect your teammates (both in the club and in a corporate setting) to sift through if they want to understand what changes you've made. To help make it easier for everyone, git allows you to attach a "message", or a description, explaining what changes you've made in the commit. For example, if you wrote some code that connects to a database, you might write something like "Implemented database connection." There are no set rules when wording your commits, but the idea is to keep them concise (short yet descriptive).

We can generate a commit log using this command.

```
git commit -m "Your message here"
```

It's a good idea to generate such a commit log after you finish working on your project for the day. Committing won't save anything on Github itself, but you'll have the changes saved to your local git repository. This can turn disasters into inconveniences. 

Once you've done a good amount of work and are ready to persist your work onto your online Github repository, you can push your code. 

```
git push origin main
```

`origin` is the remote we made earlier, and `main` is the "main" branch of our repository. We will explain branches in the next section, but what this means for us now is that we can generalize the command as such.

```
git push <remote> <branch>
```

# Branches

Git's branching feature allows you to work on separate parts of a project without affecting the main codebase. Every repository starts with a "main" branch, representing the current state of the project. Creating a new branch copies the main branch, so changes in one branch don’t affect the other. This helps teams work on different tasks simultaneously.

However, branches can diverge if multiple people make changes, which can lead to merge conflicts. To avoid this, it's best to create branches for specific features and delete them after merging back into the main branch. This keeps things manageable and reduces the risk of conflicts.

As a note of warning, you should make branches sparingly. Depending 

To make a new branch from the terminal/command prompt, type the following.

```
git branch <new branch name>
git checkout <new branch name>
```

After running these two commands, you should see some indication in the shell that you've switched branches. Now, if you make changes and commit logs, they will be in reference to this current branch instead of the main branch. To demonstrate this, go make a change to the text file we made. 

Go ahead and add/commit your changes.

```
git add -A
git commit -m "Improved text_file.txt"
```

If you see the general `git push` command from the last section, you'll see that the last argument specifies the branch you wish to push to. If your branch exists locally but not on Github, it will create that branch in Github with your new changes. Let's run that command now.

```
git push origin <your new branch>
```

If you check your Github repository on the website now, you should see that the new branch exists with your changes. 

# Making a Pull Request

Once you're done implementing your feature on your child branch, the next step is to merge this branch with its parent branch and close it. To do this, you make a "pull request" on Github that notifies whoever is in charge of the parent branch that you want to incorporate your changes into the main branch. 

On the Github website, switch to the child branch that has all your changes. Above your files, you should see a message that says `This branch is <x> commits ahead of <parent branch>.` When you click on the link, you will be taken to a page that visually shows the changes between the 2 branches. Above the change log should be a green "Create Pull Request" button. Click that and follow the instructions to make your pull request. Just like with commits, you should write a meaningful message to accompany your request. 

Once you make the pull request, switch to the parent branch and navigate to the "pull requests" tab at the top. Here, you should see the pull request you just made along with a compatibility checker that checks if the branches can be merged without issue. 
- If the compatibility checker is green, you're free to accept the pull request and finish the process.
- If you get some kind of error, though, you can either reject the pull request, which leaves the parent branch untouched, or you can accept the pull request. Accepting here means that you completely replace the parent branch's contents with the child branch's content. 

# git pull

When you have multiple sibling branches up at once, there will come a time where someone pushes their changes from a child branch to the parent branch. To ensure that the branch you're working inherits these changes properly, you can perform a "git pull" operation. It's a bit difficult to demonstrate a git pull command with just one person, so this section will discuss the general steps in case you ever need to use it in the future.

If you want to see what changes `git pull` will make to your branch, you can run this command to preview your changes.

```
git fetch
```

Fetching is optional, but it's good practice to fetch before pulling just so you see what you're pulling before you do it.

After you review the changes that will be made, you can perform the pull operation. The `git pull` command mirrors the structure of the `git push` command. 

```
git pull <remote> <branch>
```

This will pull the content from the specified branch to the current branch. So if I am in a child branch that branches off of the main branch, I would use the following.

```
git pull origin main
```

# Troubleshooting (git status)

Like with any technology, there may come a time when things don't work as expected. Git problems can be difficult to troubleshoot if you are new to the technology. Depending on your issues, though, using the following command can tell you more about the nature of your issues.

```
git status
```

This command tells you some basic information about your repositories current state, including changes you've committed and extra information about any issues you may have encountered. If you want more information, you can also run the following command which tells you even more information about your working state.

```
git log
```

This command by default uses the `vi` text editor if installed, so if you find yourself in this editor (you can't figure out how to leave), hit the escape key and type `:q` to quit. Both of these commands are useful for deducing the cause for potential issues. In any case, be sure to consider any error messages alongside the information provided by these commands, as together you're more likely to ascertain the solution yourself. 

# Forking Repositories

One important aspect of open source development is the concept of forking a repository. The idea is that you can essentially copy a repository's branch one-for-one and bring it under your domain. For example, if there exists a repository at `UserA/ReallyCoolRepository`, a forked repository would be stored at `<your account>/ReallyCoolRepository` (although the name can be changed). Forking is similar to branching in concept, but the purpose/intention is completely different. When you make a branch, the end goal is to merge the code into some higher branch and ultimately delete the branch. When you fork a repository, though, there's no way to "push" your changes back into the original repository. The idea behind forking is that you can do whatever you want to the repository without affecting the original. If you find a repository that you wish to fork, you can easily do so by clicking the "fork" button to the upper right of the `clone` button in Github. Forking is less of a core feature of git and more of a core feature for open source development as a whole. As such, you may find yourself seldom using the feature if you aren't actively contributing in the open source world.

# Conclusion

This summarizes everything we discussed during our Github Bootcamp. While this document is far from exhaustive, the commands listed here are core commands that you will find yourself using commonly as you use git. Even if you wish to use git through some visual tool (i.e. Github Desktop or VS Code's git panel), everything we discussed here is still applicable. Happy coding, and if you ever have any doubts don't hesitate to reach out to any of the FCA executive members for assistance!



