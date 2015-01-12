### Creating a repo

#### On the server ####
We start with sshing the server, and creating a bare git. Why bare? In order to
prevent overwrites from the local repos.

		$ ssh user@hostname
		$ git init --bare my-project.git 

github doesn't support shell access, so we have to use curl in order to create a
repo from command line:

	    # Taken from http://stackoverflow.com/a/10325316
	    $ curl -u 'USER' https://api.github.com/user/repos -d '{"name":"REPO"}'
		# Then clone the repo at the client, as shown below
		
#### On the client ####

	    $ git init my-project.git
		# Add remote, and push after making changes
		$ git remote add origin git@github.com:USERNAME/my-project.git
		$ git push origin master

### Cloning a repo ####
 
	    $ git clone path-to-repo.git

### Checking out a branch ###
Then there are branches of the repo, which are versions of the project. A 
project can have as many branches as required, where generally each branch adds
a new feature to the project. We can select, or create a new branch using the 
`checkout` command:

        $ git checkout branch_name  # This selects an already present branch
        $ git checkout -b branch_name # Creates a new branch and selects it

### Git File Structure ###
Every git repo has a hidden directory called .git which stores the metadata, 
and has the compressed object database. When a repo is cloned, this folder is 
copied from the remote and a local copy of the files and database is created.

When we checkout a branch, or clone a remote repo, we get what is called as
the `working directory` which contains all the files which we can modify. These 
files have been committed prior to them being available here.

Once we have a local copy of the repo, we can start making changes and, 
if required, save the changes in the database. This is usually a two step 
process, where we first add the modified files in the `staging area`.

The staging area is generally contained in your Git directory, and stores 
metadata about the files. It contains all the changes that will be pushed to 
the database during the next commit. In order to check what all changes have 
been done, we can use the `diff` command which lists the differences between 
working area and staging area.

        # lists the changes between staging area and working dir.
        # If all the changes are staged, this gives nothing
        $ git diff  
        # lists changes between staging area and last commit, use anyone:
        $ git diff --staged 
        $ git diff --cached

All the files in a git repo can be either in the tracked state, or untracked 
state. The status of the files can be checked using `status` command:

        $ git status
        On branch master
        Your branch is up-to-date with 'origin/master'.

        Changes not staged for commit:
          (use "git add <file>..." to update what will be committed)
          (use "git checkout -- <file>..." to discard changes in working directory)

                modified:   modified_file.temp

        Untracked files:
          (use "git add <file>..." to include in what will be committed)

                x.temp

        no changes added to commit (use "git add" and/or "git commit -a")

Further, every tracked file in the git repo is in one of the three stages:
* Modified: When the files have been changed but, if you commit right now these 
    changes will not be saved in the local database. 
* Staged: The files are changed, and the changes have been acknowledged. If you 
    commit right now, the changes will go to the local database. This is also 
    called the `index` of the repository. A file or directory can be staged 
    using `git add <file|directory>`
* Committed: The files are committed, i.e. all the changes that have been done 
    are now saved in the local database. 

        $ git commit 
        $ git commit -m 'message for this commit'
        $ git commit -a -m 'message for this commit'  # skips the staging area


### Branching ###

        # Creates a new branch, but doesn't check it out
        $ git branch <branch-name>  

        # Creates a new branch and checks it out as well
        $ git checkout -b <branch-name>

### Removing files from the branches, all the way ###
There are two roads that we can take here:

### Removing files from the branches, all the way ###
There are two roads that we can take here:

* Using `rm <filename>` to delete the file from the working directory. The 
    change is noted by git, but has to be staged manually using 
    `git add <filename>`.
* Using `git rm <filename>` to remove the file from the working directory and 
    index, and stop tracking it. `git rm` removes the files and stages the 
    changes. These just need to be committed.
* Using `git rm --cached <filename>` to remove it from the index but keep the 
    local file. Since the file is present in the working directory, it will 
    appear in the list of untracked files. A commit is needed. 

    



