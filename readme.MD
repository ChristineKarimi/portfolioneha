# Version Control(git)
VCS helps us organize our work and keep track of changes we make.

## Learning Goals
- Identify how to initialize a Git repository with git init
- Check the status of a repository with git status
- Keep track of file changes with git add
- Create a commit and apply a commit message with git commit
- Create a remote repository on GitHub
- Connect a local repository to a remote repository
- Set the destination of a repo with git remote
- Send code to the remote repo with git push

## Definition of terms
- repository (or repo, for short): A directory of files that are tracked by Git.
track: When a file is tracked by Git, it means that Git will notice any changes to that file. We call these changes "differences" or "diffs". Git will allow you to choose whether to add the change, or "diff," in order to keep it
- diff: Short for "difference," the "diff" of a file is all the changes that happened in it since the last commit. The "diff" of a repo is all the diffs in all the tracked files in the repo that have been made, but which have not yet been committed (sometimes programmers call this "the diffset").
- commit: When a diff is decided to be a good thing to save, we commit the diff to the repo's history using the commit command. When we make a commit we are asked to write a "log" message which describes what happened in the diff. Each commit also knows when it happened and what the repo's "diff" was.
- log: The record of what happened in each commit
- local/remote: When we start working with a git repo, we "clone" it from a remote source and have a copy of that directory on our own system. We call the repo on our personal system the local repo. (We'll talk more about the "clone" command later.)
- default branch: You'll learn in advanced Git that a repo can support multiple branches (we called those "sandboxes" earlier). For the moment, just remember this: by default, when you create a Git repo, you will be working on the default branch. The name of this branch may be either main or master, depending on your configuration.
- branch: The combined history of all the changes of all the files in the repo.

## Benefits of git as a VCS
- Automatically create a backup of your work
- Provide an easy way to undo mistakes and restore a previous version of your work
- Document changes, including a log of what's changed with messages explaining why it was changed
- Keep file names and hierarchies consistent and organized
- Branch work off into multiple "sandboxes" that can be experimented with but won't impact each other
- Collaborate with others without disturbing each other's or our own work

## How to Initialize a Git Repository with git init
Git operates on a directory level. When we have a new directory that we want to track our files in, we need to initialize the directory as a Git repository. That means Git will then pay attention to what goes on in the directory and give us all the Git superpowers.

- To get started, we'll create a new directory. In your terminal, type the following:

REMEMBER: Don't type the $. That's the universal symbol for a command prompt. It's how technical documentation says "Here's a thing for the shell to process."

 `mkdir my-git-project`
This command creates new a directory. Then:

 `cd my-git-project`
This command moves into the newly created directory.

- Now that we're in the directory where we want Git to watch for changes (adding, removing, and editing files), let's set up this directory by initializing it. In the terminal type git init. It should look like this:

 `git init`
Initialized empty Git repository in /Users/avi/my-git-project/.git/

Git lets us know that it has put /Users/avi/my-git-project under its protection. Git also tells us that it stores its own data in the .git directory. This hidden directory, .git, is where Git keeps important stuff, like the commit history. Don't go in there and start randomly deleting things! That said, if ever you do git init in the wrong directory, you can rm -rf .git and return the directory to a plain-old, unprotected directory.

Be careful about making an entire directory, like our home directory or our desktop, into a Git repository accidentally. Make sure you only type git init within the directory you want git to track.

- Check the Status of a Repository with git status
Now that we have Git watching this directory, let's see what it can tell us about the directory. The command we use for this is git status.

 `git status`
Since we have not added any files yet, we'll see:

On branch main

No commits yet....

- Let's create a README.md that describes the project. Make our new file by typing touch README.md from within the my-git-project directory. We won't see any output after touch, but we will see a new file has been created if we type ls (which gives a list of all the files in the directory).

 `touch README.md`
 `ls`

README.md
With at least one new project file we can enable Git to start tracking changes. Type git status. Git will show us what our current repository looks like and what changes it sees.

 `git status`
On branch master

No commits yet

Untracked files:
..." to include in what will be committed)

  README.md

nothing added to commit but untracked files present (use `git add` to track)
Git confirms that it's aware of the file README.md, but it's not "tracking" it. Git's not doing anything with the file and the file is not doing anything with Git...yet. Let's change that!

IMPORTANT: Whenever we want to check the status of our Git repository — which we do often — type git status.

- Keep Track of File Changes with git add
Currently, the file in our repository is not being tracked by Git. We have to tell Git about all the files we want it to keep track of and consider as part of our project. We can do this by adding the files to our git repository with git add <filename or path>. To add our new README.md to the repository and check the status, we type:

 `git add README.md`
 `git status`
On branch master

No commits yet

Changes to be committed:
..." to unstage)

  new file:   README.md
We can now see that Git is ready to keep track of README.md. All the changes in the file at the time we added it are "staged." If we were to change README.md, we'd need to re-add the file. As it happens here, this staged change is "create the file, nothing inside of it" because touch created an empty file.

To save a new version of this new file (or, later, to "capture" changes to a file) we need to commit the set of changes or "diff." We "save" the changes in our repository by making commits.

- Create a Commit and Apply a Commit Message with git commit
Remember: git add got our changes to the repository ready in the previous step. Those changes are the ones that will be "captured" in the commit.

To make our first commit, type:

 `git commit -m "Initial commit"`
This tells git that our commit message, represented by the -m flag, is "Initial commit".

 git commit -m "Initial commit"
[main (root-commit) e55477d] Initial commit
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 README.md
We can see that Git has created a new version of our repo, represented by the SHA e55477d. SHAs are the identification system that git uses to keep track of versions; they're long complex numbers and letters that are unlikely to be duplicated.

The commit command committed 1 file.

- Now, if we type git status, we'll see that it is at a "clean state", and there is nothing to commit and no new changes.

 `git status`
On branch master
nothing to commit, working tree clean
If we make another change, for example, to README.md, we can add another commit with this new set of changes with

 `git commit -am "Updates README.md"`
- The use of the -am flag here is a shortcut that combines the steps of adding changed files and committing them. The -a flag tells git to add 'all changes', i.e., all files that have been changed since the last commit. The -m flag, like before, tells git that we want to specify a commit message, in this case, "Updates README.md". To review some of your Unix CLI skills, this could also be written as:

 git commit -a -m "Updates README.md"
The commit would look like:

 git commit -am "Updates README.md"
[main (root-commit) e55477d] Updates README.md
 1 file changed, 4 insertions(+), 0 deletions(2)


## Create a Remote Repository on GitHub
- There are a few steps to follow to create a remote repository on GitHub.

- Go to: `github.com/new` (Links to an external site.), while logged into GitHub.

- Enter a name for your repository in the "Repository name" field. You can name it whatever you'd like; be creative! The default options are fine as-is — don't initialize the new repository with a README or add a .gitignore or license. Click the green 'Create repository' button.

- After you create the remote repository, you should see a "Quick setup" page. Make sure the 'SSH' option is selected, then click the "Copy to clipboard" symbol next to the repo URL (pictured) to copy the URL. (We'll use this in the next section.)


Behind the scenes, GitHub has essentially git init'd a blank directory.

- Connect a Local Repository to a Remote Repository
After you've created your remote GitHub repository, you'll want to get your local repository uploaded to GitHub. Follow the steps below:

- First, we want to create a folder for our repository, which we'll call my_new_directory. In the terminal, navigate to the ~/Development/code directory (or wherever you are storing your code) and type mkdir my_new_directory.

- To navigate into this new folder, type cd my_new_directory. Your terminal should display my_new_directory, indicating that you are now inside of the new folder. Open the directory in VS Code by typing code ..

- Next, we need to create a new file named README.md. You can do this in the terminal, by typing touch README.md, or in VS Code, by choosing File -> New File.

- We can directly type in content for our README file in VS Code, but we can also use our terminal skills to add content. So, in the terminal, type echo "This is my readme file" > README.md. If you've got the README file open in VS Code, the new text will appear!

- Now that we've got some basic content, we can initialize our local repository. In your terminal, type git init. Your terminal should show that an 'empty Git repository' has been initialized.

- Type `git add README.md` to stage the new README.md file so it will be tracked by git.

Now, type `git commit -m "Initialize git"`. This will create the first commit for this local repository, which will allow us to push our work to the remote repository we created earlier.

- Set the Destination of a Repo with git remote
To connect your local repository to the newly created GitHub repository, you must add a new remote to a remote name. Adding a remote involves giving git a "short name" and a "repository path." You copied the repository path from GitHub a few steps above.

- The repository path is a long bunch of technical words. The creators of Git thought it would be easier to type a "nickname" or a "short name" that points to that long repository path. It's common to have a "default" remote. The default remote short name is called origin. So we're going to create a new remote with a short name of origin.

- Make sure you still have your remote Git info copied from GitHub, and type the following into the terminal:

 `git remote add origin your-copied-remote-repository-url`
This sets the remote so you can now push your code.

* You can use git remote -v (the -v is for "verbose") to view the remote(s).

 `git remote -v`
- View existing remotes
* origin  git@github.com:OWNER/REPOSITORY.git (fetch)
* origin  git@github.com:OWNER/REPOSITORY.git (push)

- Send Code to the Remote Repo with git push
Now that we have added a remote repo, we need to send our latest work to the remote. We use this command when we want to send some code from the local repository to the associated remote repository. Git will push all the local, committed work to the remote repository.

The git push command takes two arguments. The first is the name of the remote repo. Remember, origin is just an alias or "short name" that refers to the repository name. You don't actually have to enter the repository name. Instead, you can just use origin. The second is the name of the remote branch you want to send code to. In the example below, we're pushing to our remote repository's default branch.

Depending on your system configuration, your default branch's name might be either main or master. You can find out what the default branch for your current repository is by running:

 `git branch --show-current`
Whatever the branch listed in the terminal is will be your default branch (it should be either master or main).

If your default branch name is master, run this command to push your code up to GitHub:

 `git push -u origin master`
Otherwise, if your default branch name is main, run this command to push your code up to GitHub:

 `git push -u origin main`
This will push your code up to the remote repo/branch. The first time you push code up to a newly-added remote repository, use the -u flag to tell Git to "save" the remote repository as the default push destination for your current branch.

For every subsequent push, you only need to enter git push.

- An Aside and a Small Shortcut
In this lesson, we've gone through the steps of both connecting a local repository, and pushing code up to GitHub. During this course, you'll be creating a few local repositories from scratch, but more often, you'll be cloning existing repositories to your local machine. In these situations, you won't need to use commands like git init, since the repo is already set up with Git and will already have a remote configured. However, you will often need to add, commit and push work you've done locally to the remote repository. In these situations, you should be able to just run the following commands:

 `git add .`
 `git commit -m "commit message"`
 `git push`

- As a small shortcut, you can also combine adding all tracked files and committing by using an additional option flag, -a, with the commit command:

 `git commit -am "commit message"`
 `git push`
- Note that the -am flags will work for adding and committing changes to existing tracked files, but if you need to create a new file as part of any lesson, you'll need to use git add to track that file before committing.


# Conclusion
To make a new Git repository out of a directory — which we'll only have to do once per project — use git init. Whenever you make a change to a file or create a new file, you can check the status of these changes with git status. When you're ready to preserve changes, you can add the files (or directories of files) with the git add <filename or path> command.

Once your changes have been added, or "staged," use `git commit -m` to commit them with an explanatory message. You can shorten the add + commit process, provided that all the files are being tracked, by using `git commit -am "A message"`.

Being able to add Git remotes allows you to back up your local repository to a remote server. If you remember git init, git remote add origin your-remote-repository-URL, add, and push your changes, you'll be able to get your project up to GitHub in minutes!