### Creating a repo

#### On the server
We start with sshing the server, and creating a bare git. Why bare? In order to
prevent overwrites from the local repos.

		$ ssh user@hostname
		$ git init --bare my-project.git 

github doesn't support shell access, so we have to use curl in order to create a
repo from command line:

	    # Taken from http://stackoverflow.com/a/10325316
	    $ curl -u 'USER' https://api.github.com/user/repos -d '{"name":"REPO"}'
		# Then clone the repo at the client, as shown below
		
#### On the client

	    $ git init my-project.git
		# Add remote, and push after making changes
		$ git remote add origin git@github.com:USERNAME/my-project.git
		$ git push origin master

### Cloning a repo

	    $ git clone path-to-repo.git
