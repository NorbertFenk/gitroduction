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
The "Changes to be committed" text indicate that it is in ***staged*** state. In this state if you commit the changes what you have done so fare, Git will make a new commit with the given commit message. On the other hand if you do not commit it you can make furhter changes on the *first.txt* file. Please modify the content of the *first.txt*.
```
echo "Hello world" > first.txt
```
In this case if you use tha ***git status*** command once again you will se something similar to this:
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
To check the commits use this command.
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






















