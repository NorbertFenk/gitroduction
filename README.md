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

* Analyze the git-lifecycle image :heavy_check_mark:

* Learned how to add files to Git :heavy_check_mark:

* Learned how Git handles modifications :heavy_check_mark:
 
* Learned how to commit changes from the command line :heavy_check_mark:

* Learned how to remov files from Git :heavy_check_mark:

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
  
  * **git checkout < file >** to discared changes on a modified file  :heavy_check_mark:














