# gitroduction
Yet another beginner guide to git.

## [A brief history of version control](https://www.red-gate.com/blog/database-devops/history-of-version-control)

The relatively new computer indsutry did not invent version control. It adopted practicies that were well established in industrial manufacturing and design, where complex machines such as aircrafts, tanks, cars required more than one discipline, particularly in the technical drawing of components. Over the engineering process they change the drawings and specifications as required, givin each version of every component a version number.
Software soon followed this process but there were numerous limits at that time e.g they had to use punched cards. The work was treated as if it were a technical drawing. To alter a version, you checked the code in and out as though it were a technical drawing that had to be altered.
As soon as programs became text files, the manual process were automated using programs such as Source Code Control System ([SCCS](https://en.wikipedia.org/wiki/Source_Code_Control_System)). The technology was there but it was not ready.

**Centralized**

The original version control software was mainframe-based and individual programmers accessed the system via a terminal.UNIX systems were the first to introduce server-based, or centralized version control systems that relied on a single, shared repository. These systems were worked well if the team co-located on the same file-sharing server, they were useless where some of the team were outside the domain. In the mid-nineties, version contorl became network-based but still hosted on a server.

**Distributed**

In the distributed model no single computer held the master copy. The model of Distributed Version Control Systems ([DVCS](https://en.wikipedia.org/wiki/Distributed_version_control)) became mainstream with [BitKeeper](http://www.bitkeeper.org/), followed by [Git](https://git-scm.com/) and [Mercurial](https://www.mercurial-scm.org/) and it made the process of forking, branching and merging far easier.
DVCS do not necessarily rely on a central server. Instead, every developer 'clones' a copy of the repository and has a full history of the project on their own machine. When they get new changes from repository, they 'pull' them. When they commit their own changes they need to 'push' it to make available for the rest of the team.

This section is based on the following article: https://www.red-gate.com/blog/database-devops/history-of-version-control

## [Short history of Git](https://git-scm.com/book/en/v2/Getting-Started-A-Short-History-of-Git)

The Linux kernel is an open source software with a quite large scope. Until 2002 the changes were passed around as patches and archived files. In 2002 the project began using a DVCS called [BitKeeper](http://www.bitkeeper.org/).
In 2005, the relationship between the community and the commercial company broke down, and the tool's free-of-charge status was revoked. This prompted the Linux community and in particular [Linus Torvalds](https://hu.wikipedia.org/wiki/Linus_Torvalds) to develop their own tool.

Little more about it: https://git-scm.com/book/en/v2/Getting-Started-A-Short-History-of-Git

## Git in practice 

### Installation and basic configuration
Installation:
Go to https://git-scm.com/downloads and select your OS
Follow the instructions there to install Git

[Hint](https://askubuntu.com/a/568596) for Ubuntu users:
```
sudo apt-add-repository ppa:git-core/ppa
sudo apt-get update
sudo apt-get install git
```

To check your git version use this command.
```
git --version
```
Set your username and email for better raging experience. :smile: Joke aside, Git uses a username to associate commits with an identity.
```
git config --global user.name "John Doe"
git config --global user.email johndoe@example.com
```
Alternatively you can edit the .gitconfig file where you can also set many other paramters. If you don't know where is your ***.gitconfig*** you can check the file location with this command.
```
git config --list --show-origin
```
Tested with Git 2.14.1 but according to this [stackoverflow answer](https://stackoverflow.com/a/2115116/5789008) it works since version 2.8.

### Starting from scratch
To initialize a new git repository use the following commit
```
git init
```
This command creates an empty Git repository - basically a .git directory with subdirectories, The contet of these directories is not part of this begginer guide but if you would like to read about it you can check this [link](https://git-scm.com/docs/git-init). **NOTE**: Running ***git init*** in an existing repository is safe. It will not overwrite things that are already there.

#### The lifecycle of the status of your files

![alt text](https://github.com/NorbertFenk/gitroduction/blob/master/git-lifecycle.png)

#### Add files to Git
Please do the following instructions to get some hands-on experience.
So you have a folder which is a git repository if you used the ***git init*** command.
Make a new empty file e.g. with the following command.
```
touch first.txt
```
At the moment you have an **untracked file** named **first.txt**. To make sure it is realy untracked on your computer write the following command to your terminal.
```
git status
```
You should see something like this as an output.
```
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	first.txt

nothing added to commit but untracked files present (use "git add" to track)
```
Untracked basically means that Git sees a file you didn't have in a previous snapshot (commit). Git won't start including it in your commit snapshot until you explicitly tell it to do so. E.g.: It will prevent to accidentally begin including generated binary files.
To track a new file you should use the ***git add*** command. In this case we would like to track the *first.txt*.
```
git add first.txt
```
If you run ***git status*** command again you can see your *first.txt* file is now tracked and staged to be committed.
```
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

	new file:   first.txt
```
The "Changes to be committed" text indicate that it is in ***staged*** state. In this state if you commit the changes what you have done so far, Git will make a new commit with the given commit message.

#### Modify files
On the other hand, if you do not commit it you can make furhter changes on the *first.txt* file. Please modify the content of the *first.txt*.
```
echo "Hello world" > first.txt
```
In this case if you use the ***git status*** command once again you will se something similar to this:
```
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

	new file:   first.txt

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   first.txt
```
What you see here is that you have added the *first.txt* to the staging area but modify it so Git detect the changes. To move on this state you can use the ***git add first.txt*** command again it should results the next state.
```
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

	new file:   first.txt
```

#### Commit changes
Please make our first commit with this command.
```
git commit -m "hello"
```
After that you should see similar output with different commit id.
```
[master (root-commit) f36d68c] hello
 1 file changed, 1 insertion(+)
 create mode 100644 first.txt
```
To check the commits use this command. More details about **git log** [here](https://git-scm.com/book/en/v2/Git-Basics-Viewing-the-Commit-History)
```
git log
```
It will print out all the commits in this repository. At the moment you should see something like this.
```
commit f36d68cfbae3ebf3337f70b429fdd3e095f70c9a (HEAD -> master)
Author: <Author Name> <authorname@xyz.com>
Date:   Fri May 18 00:15:49 2018 +0200

    hello
```
Congratulations, you have done your first commit with Git. 

#### Removing files
To remove a file from Git, you have to remove it from your tracked files (more accurately, remove it from your staging area) and then commit. The ***git rm*** does that, and also remove the files from your working directory so you do not see it as an untracked file the next time.
Please do the following steps below:
1. ```echo "Delete me from working directory with git rm command" > delete-me.txt```
2. ```git add delete-me.txt```
3. ```git commit delete-me.txt -m "delete-me.txt commited"```
4. ```git rm delete-me.txt```

If you use ***git status*** in this state you should see something similar to this.
```
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	deleted:    delete-me.txt
```
The next time you commit, the file will be gone and no longer tracked. If you modified the file and added it to the staging area already, you must force the removal with the -f option. This is a safety feature.

#### CHECKPOINT 1.:

* Analyzed the git-lifecycle image :heavy_check_mark:
* Learned how to add files to Git :heavy_check_mark:
* Learned how Git handles modifications :heavy_check_mark:
* Learned how to commit changes from the command line :heavy_check_mark:
* Learned how to remove files from Git :heavy_check_mark:

#### git diff
If the ***git status*** command is too vague for you — you want to know exactly what you changed, not just which files were changed — you can use the git diff command. You’ll probably use it most often to answer these two questions: What have you changed but not yet staged? And what have you staged that you are about to commit? Please follow this short example below.

##### What have you changed but not yet staged case
1. echo "asd asd asd" > git-diff-me.txt
2. git add git-diff-me.txt 
3. echo "asererererereer" >> git-diff-me.txt

To see what you’ve changed but not yet staged, type ***git diff*** with no other arguments:
If you done with commands, you should see something similar
```
diff --git a/git-diff-me.txt b/git-diff-me.txt
index 93255a5..11e722b 100644
--- a/git-diff-me.txt
+++ b/git-diff-me.txt
@@ -1 +1,2 @@
 asd asd asd
+asererererereer
```
##### What have you staged that you are about to commit case
Assume the previous state, if you use this ***git diff --staged*** you should get an output like this.
```
diff --git a/git-diff-me.txt b/git-diff-me.txt
new file mode 100644
index 0000000..93255a5
--- /dev/null
+++ b/git-diff-me.txt
@@ -0,0 +1 @@
+asd asd asd
``` 
This command compares your staged changes to your last commit. It’s important to note that git diff by itself doesn’t show all changes made since your last commit — only changes that are still unstaged. **If you’ve staged all of your changes, git diff will give you no output.**

#### .gitignore
Often, you’ll have a class of files that you don’t want Git to automatically add or even show you as being untracked. These are generally automatically generated files such as log files or files produced by your build system. In such cases, you can create a file listing patterns to match them named .gitignore. Setting up a .gitignore file for your new repository before you get going is generally a good idea so you don’t accidentally commit files that you really don’t want in your Git repository.
A little example to .gitignore:
1. write a simple hello world program in C++
```
#include <iostream>

int main()
{
	std::cout << "Hello world" << std::endl;
	return 0;
}
```
2. ```echo "*.[oa]" > .gitignore```
3. ```g++ -c hello.cpp``` This will produce a hello.o file
4. ```git status```
```
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)

	.gitignore
	hello.cpp

nothing added to commit but untracked files present (use "git add" to track)
```
There is no **hello.o** file. On the other hand, if you remove the **.gitignore** file with
``` rm .gitignore``` then use the ***git status*** command, you will get this output.
```
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)

	hello.cpp
	hello.o

nothing added to commit but untracked files present (use "git add" to track)
```
Here you can find some very useful .gitignore examples: https://github.com/github/gitignore

#### Undoing things
At any stage, you may want to undo something. Here, we’ll review a few basic tools for undoing changes that you’ve made.

##### Forget something to commit -> git commit --amend
One of the common undos takes place when you commit too early and possibly forget to add some files, or you mess up your commit message. This case ***git commit --amend*** may help you out.
1. ```echo "*.[o]" > .gitignore```
2. ```git add .gitignore hello.cpp```
3. ```git commit -m "add helloworld program and .gitignore"```
This point we realize we forgot some file.
4. ```echo "forgotten txt" >> forgotten.txt```
5. ```git add forgotten.txt```
6. ```git commit --amend``` This command will open a text editor where you should see something like the block below. Here you can rewrite the commit message and check the files to be commited.
```
add helloworld program and .gitignore

# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# Date:      Mon May 21 10:53:05 2018 +0200
#
# On branch master
# Changes to be committed:
#       new file:   .gitignore
#       new file:   forgotten.txt
#       new file:   hello.cpp
#
````
7. After you exit from the editor should see this output
```
[master 13905f6] add helloworld program and .gitignore
 Date: Mon May 21 10:53:05 2018 +0200
 3 files changed, 9 insertions(+)
 create mode 100644 .gitignore
 create mode 100644 forgotten.txt
 create mode 100644 hello.cpp
```
The **amend** command takes your staging area and uses it for the commit. If you’ve made no changes since your last commit (for instance, you run this command immediately after your previous commit), then your snapshot will look exactly the same, and all you’ll change is your commit message.

##### Unstaging a Staged file
Let’s say you’ve changed two files and want to commit them as two separate changes, but you accidentally type git add * and stage them both. How can you unstage one of the two? The git status command reminds you:
1. ```echo "file should be commited" >> commit-me.txt```
2. ```echo "file should not be commited" >> do-not-commit-me.txt```
3. ```git add *```
```
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	new file:   commit-me.txt
	new file:   do-not-commit-me.txt
```
4. The answer is in the ***git add***'s output: use the ```git reset HEAD do-not-commit-me.txt``` command.
```
On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	new file:   commit-me.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	do-not-commit-me.txt
```
The command is a bit strange, but it works.
5. Commit the **commit-me.txt** to make proper state for the next section.
``` git commit -m "add commit-me.txt" && rm do-not-commit-me.txt```

##### Unmodifying a Modified File
1. ```git status```
```
On branch master
nothing to commit, working tree clean
```
2. ```echo "Additional lines" >> commit-me.txt```
What if you realize that you don’t want to keep your changes to the **commit-me.txt** file? Luckily, git status tells you how to do that, too.
This is our ***git status*** output at the moment:
```
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   commit-me.txt

no changes added to commit (use "git add" and/or "git commit -a")
```
3. ```git checkout commit-me.txt``` will discard our changes as it described the output above
4. Our ***git status*** output looks like this:
```
On branch master
nothing to commit, working tree clean
```

#### CHECKPOINT 2.:

* Learned about **git diff** command :heavy_check_mark:
* Wrote our first **.gitignore** file :heavy_check_mark:
* Learned how to undo things in different stages :heavy_check_mark:
  * **git commit --amend** to add and modify things after commit :heavy_check_mark:
  * **git reset HEAD < file >** to unstage staged files  :heavy_check_mark:
  * **git checkout < file >** to discard changes on a modified file  :heavy_check_mark:
  
**Sources**:
The checkpoint 1 and 2 contains information [from](https://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository) here to [this](https://git-scm.com/book/en/v2/Git-Basics-Undoing-Things).

### [Working with Remotes](https://git-scm.com/book/en/v2/Git-Basics-Working-with-Remotes)
To be able to collaborate on any Git project, you need to know how to manage your remote repositories. Remote repositories are versions of your project that are hosted on the Internet or network somewhere.

#### Showing your remotes
To see which remote servers you have configured, you can run the git remote command. If you use this command in our training repository there will be no output because there is no remote server to that repository. To continue the training we should get somehow a repository with remotes. To achieve this please follow the instructions below.
1. ```cd ..```
2. ```git clone https://github.com/schacon/ticgit```
```
Cloning into 'ticgit'...
remote: Counting objects: 1857, done.
remote: Total 1857 (delta 0), reused 0 (delta 0), pack-reused 1857
Receiving objects: 100% (1857/1857), 331.41 KiB | 737.00 KiB/s, done.
Resolving deltas: 100% (837/837), done.
```
If you’ve cloned your repository, you should at least see **origin** — that is the default name Git gives to the server you cloned from.
```
cd ticgit
git remote
origin
```
You can also specify -v, which shows you the URLs that Git has stored for the shortname to be used when reading and writing to that remote:
```
git remote -v
origin	https://github.com/schacon/ticgit (fetch)
origin	https://github.com/schacon/ticgit (push)
```
#### Inspecting remote
If you want to see more information about a particular remote, you can use the **git remote show < remote >** command. In our case we should get this output:
```
* remote origin
  Fetch URL: https://github.com/schacon/ticgit
  Push  URL: https://github.com/schacon/ticgit
  HEAD branch: master
  Remote branches:
    master tracked
    ticgit tracked
  Local branch configured for 'git pull':
    master merges with remote master
  Local ref configured for 'git push':
    master pushes to master (up to date)
```
#### Fetching and pulling from Your remotes
As you just saw, to get data from your remote projects, you can run:
``` git fetch <remote> ```
The command **goes out** to that remote project and **pulls down** all the **data** from that remote project that **you don’t have yet**. If you clone a repository, the command automatically adds that remote repository under the name “origin”. So, ```git fetch origin``` fetches **any new work** that has been pushed to that server **since you cloned (or last fetched from) it**.

:bangbang: ***It’s important to note that the ```git fetch``` command only downloads the data to your local repository — it doesn’t automatically merge it with any of your work or modify what you’re currently working on.*** :bangbang:

We will discuss later about branches but worth to mention the next statement.
If your current branch is set up to track a remote branch, you can use the ```git pull``` command to **automatically fetch and then merge** that remote branch into your current branch.

#### Pushing to your remotes
When you have your project at a point that you want to share, you have to push it upstream. The command for this is simple: ```git push <remote> <branch>```. This command works only if you cloned from a server to which you have write access and if nobody has pushed in the meantime. If you and someone else clone at the same time and they push upstream and then you push upstream, your push will rightly be rejected. You’ll have to fetch their work first and incorporate it into yours before you’ll be allowed to push.

#### Hands-on section
1. Any of this three account would be fine:
    * github
    * bitbucket
    * gitlab
2. Add your ssh key: e.g. https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/
3. https://help.github.com/articles/creating-a-new-repository/ To avoid errors, do not initialize the new repository with README, license, or gitignore files.
4. At the top of your GitHub repository's Quick Setup page, click to copy the remote repository URL. 
5. ```git remote add origin remote repository URL```
6. ```git push origin master```
```
Counting objects: 14, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (8/8), done.
Writing objects: 100% (14/14), 1.20 KiB | 614.00 KiB/s, done.
Total 14 (delta 1), reused 0 (delta 0)
remote: Resolving deltas: 100% (1/1), done.
To github.com:NorbertFenk/asd.git
 * [new branch]      master -> master
Branch master set up to track remote branch master from origin.
```

#### CHECKPOINT 3.:

* Check repository remotes :heavy_check_mark:
* Fetching pulling and pushing changes :heavy_check_mark:
* Create a github user :heavy_check_mark:
* Register your ssh key to it :heavy_check_mark:
* Pushing our work to a remote github server :heavy_check_mark:

