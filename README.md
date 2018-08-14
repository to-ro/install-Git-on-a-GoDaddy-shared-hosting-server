# install-Git-on-a-GoDaddy-shared-hosting-server
How to install Git on a GoDaddy shared hosting serverinstall Git on a GoDaddy shared hosting server

## This is for a Linux shared hosting account with GoDaddy.

## Install Git on your GoDaddy shared hosting server
Server does not come with git pre-installed. Therefore you need to SSH to your server and download/unpack Git. You can set-up your SSH access by following these instructions provided by GoDaddy.

### 1. Open Terminal and login to your hosting account:

`$ ssh yourusername@yourserver`
`$ yourpassword`

Note: To prevent having to enter your password every time you SSH to your server, set-up SSH key authentication. For anyone unsure how SSH keys work, GoDaddy explain this pretty well:

The public and private key are similar to a puzzle. They are created together to use during the login/authentication process. The public key resides on the server (the remote location) The private key resides locally on your computer/server. When you attempt to login to a server, the public and private key are compared. If they “match”, then you will be allowed to login to the server location.

### 2. Download the GIT binaries:

$ wget http://adamboother.com/assets/downloads/git-1.7.3.4_centos5.2.tar.bz2
These binaries have been compiled from Git (version 1.7.3.4) on a Linux machine running CentOS 5.2, which is the same operating system that my GoDaddy server runs. Linux binaries are usually portable so these might also work on other servers running a different operating system. If they don’t work, you can compile them yourself using a virtual machine with the same operating system specifications as your hosting account.

### 3: Unpack the downloaded Git binaries:

$ tar -xvjf git-1.7.3.4_centos5.2.tar.bz2
Set up the Git repository
So now Git is installed on your server, you can go ahead and create a Git repository. Let’s say we’re going to create this repository in the home directory:

1. Go to the home directory:

$ cd ~/public_html
1. Initialise your Git repository:

$ git init
3. Change the permissions to protect your git repository, as it will be visible on the web:

$ chmod 770 -R .git
4. Accept pushes from your local repository:

$ git config receive.denyCurrentBranch ignore
5. Go to the ‘hooks’ directory then edit the ‘post-receive’ file:

$ cd .git/hooks
$ nano post-receive
Add the following into top of file:

GIT_WORK_TREE=../ git checkout -f
Save these changes to the file and exit it.

6. Change the permissions for this file:

$ chmod +x post-receive
That’s your Git repository set-up and all the necessary housekeeping done.

Clone your Git repository to your machine
Git is now installed on your server and you’ve set-up the repository for your site. You now need to clone this repository to your machine. To keep this tutorial simple, we’re going to clone this repository onto the desktop.

1. Open a new tab in your command line editor, then go to the desktop directory:

$ cd ~/Desktop
2. Clone your live respository:

$ git clone yourusername@yourserver:public_html
3. Add your site files to your local folder, then commit/push them up to the server:

$ git add -A
$ git commit "Your commit message here"
$ git push origin master
Your local files are now up on your server and you’re good to go. Any amendments to your site from now on will be tracked and can be pushed up to your GoDaddy shared hosting server using Git.
