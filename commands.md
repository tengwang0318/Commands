### modify hosts to block some websites



sudo vi /etc/hosts

# Git

### Getting a Git Repository

there are two ways to obtain a Git repository:

1. taking a local directory that is currently not under version control, and run the command ```git init ```.
2. Cloning an existing Git repository from anywhere by using the command ```git clone ```.

#### Initializing a Repository in an Existing Directory

1. cd to the directory where you want to control.
2. run the command ```git init```, then you will get a **new** subdirectory named **.git** that contains all of information. After running this command, you could track all of files which are in the directory.

#### Cloning an Existing Repository

Just run ```git clone <url> ```, then Git will receive a full copy of nearly all data that the server has, even the history of the project.

##### Specify the Project's Name by Cloning

Running the command``git clone https://github.com/xxx/abc myProject`` to revert the name of the project that is on the server to **myProject**.

### Recording Changes to the Repository

Each file in working directory can be in one of two states: tracked or untracked.

Tracked file are files that were in the last snapshot, as well as newly staged files; they could be unmodified, modified, or stages. 

![the life cycle of the status of your files](pic/1.png)

#### Checking the Status of Your Files

``git status``

This command definitely could give you some tips, such as how to reset, what could you do next, and etc.

running `git status -s`  or `git status --short`, you will get a far more simplified output. 

`??`: are new files and not tracked.

`A`: new files that have been added to the staging area

`M`:modified files

`MM`:modified, staged and then modified again



#### Viewing Staged and Unstaged Changes

`git diff` compares what is in your working directory with what is in your staging area.

`git diff --staged` compares your staged changes to your last commit. The command equal to `git diff --cached`(`--staged` and `--cached` are synonyms).



#### Commit Changes

`git commit -m <message>`

#### Skipping the Staging Area

If you want to skip the staging area, run `git commit -a` which will automatically stage every file that is already tracked before doing this commit.

#### Removing Files

To remove a file from Git, you have to remove it from your tracked files(more accurately, remove it from your staging area) and then commit. `git rm` command does that, and also removes the file from your working directory so that you don't see it as an untracked file next time. (**Don't forget COMMIT!!!**)

If the file which was modified and added to the staging area, you must force the removal with the **-f** option.

If you want to remove a file which has been tracked from the staging area and don't want to remove from the working directory, run the command `git rm --cached <filename>`. It's particularly useful when you forget add something to your **.gitignore** file and accidentally staged it.

#### Moving Files

Git doesn't explicitly track file movement.

Rename: `git mv file_from file_to`. This is equivalent to running like this:

```git
mv file_from, file_to
git rm file_from
git add file_to
```





### Ingoring Files

Some files, like log files, do not need to be tracked, because it is meaningless.

In a file named `.gitignore` which follows the rules of RegExp, Git will ignore these files which follow the pattern in `.gitignore`

- Blank lines or lines starting with # are ignored.
- Standard glob patterns work, and will be applied recursively throughout the entire working tree.
- You can start patterns with a forward slash (/) to avoid recursivity.
- You can end patterns with a forward slash (/) to specify a directory.
- You can negate a pattern by starting it with an exclamation point (!).





### Viewing the Commit History

`git log` lists the commits made in the repository in reverse chronological order. The command lists each commit with its **SHA-1 checksum**, **Author Name**, **email, Date & commit message**.

`git log -p` or `git log --patch` shows the difference introduced in each commit. You could limit the number of log entries displayed, such as using **-2** to show only the last two entries.

running `git log --stat`, if you want to see some abbreviated stats for each commits.

`--pretty` could change the formats of default output.

#### Limiting Log Output

The time-limiting options such as **--since** and **--until** are more practical than **--<n>**.

`git log --since=2.weeks`: the list of commits made in the last two weeks.

**--author** allows you to filter on a specific author

The detail should check in the official documents.

### Undoing Things

One of the common undos takes place when you commit too early and possibly forget to add some files, or you mess up your commit message. If you want to redo that commit, make the additional changes you forgot, stage them, and commit again using the **--amend** option:

```
git commit --amend
```



#### Unstaging a Staged File

Just let `git status` tell you the solution: `git reset HEAD <file>`

#### Unmodifying a Modified File

Revert a modified file to the last committed. 

**Again,** let `git status` tell you the solution: `git checkout -- <file>`



Anything that is committed in Git can always be recovered. 



#### Undoing Things with Git Restore

##### Undoing a Staged File with Git Restore

```
git restore --staged <filename>
```

##### Unmodified a Modified File with Git Restore

``` 
git restore --staged <filename>
```

### Working with Remotes





``git remote`` will show all of remote servers you have configured. It lists the shortnames of each remote handle you've specified. 

`git remote -v` will show you the URLs that Git has stored for the short name to be used when reading and writing to that remote.

#### Adding Remote Repositories

`git clone` command implicitly adds the **origin** remote to you.

To add a new remote Git repository as a shortname you can reference easily, run `git remote add <shortname> <url>`

If there is a remote server whose shortname is pb, then you could run `git fetch pb` to fetch all the information that pb has but that you don't have yet in your repository. 

What's more, pb's `master ` branch is now accessible locally as pb/master.

#### Fetching and Pulling from Your Remotes

`git fetch <remote>`

After doing this, you should have references to all teh branches from that remote, which you can merge in or inspect at any time.

If you clone a repository, the command automatically adds that remote repository under the name **origin**. So, `git fetch origin` fetches any new work that has been pushed to that server since you cloned (or last fetched from) it. It’s important to note that the `git fetch` command only downloads the data to your local repository — **it doesn’t automatically merge it with any of your work or modify what you’re currently working on**. **You have to merge it manually into your work when you are ready.**

If your current branch is set up to track a remote branch, **you can use the `git pull` command to automatically fetch and then merge that remote branch into your current branch**. This may be an easier or more comfortable workflow for you; and by default, the `git clone` command automatically sets up your local master branch to track the remote master branch (or whatever the default branch is called) on the server you cloned from. Running `git pull` generally fetches data from the server you originally cloned from and automatically tries to merge it into the code you’re currently working on.



#### Pushing to Your Remotes

`git push <remote> <branch>`

#### Inspecting a Remote

`git remote show <remote>` shows more information about a particular remote.

#### Renaming and Removing Remotes

`git remote rename <old_name> <new_name>`

`git remote remove` or `git remote rm`

### Tagging

#### Listing Your Tags

`git tag` (with optional `-l` or `--list`)

#### Creating Tags

Git supports two types of tags: **lightweight** and **annotated**.

A **lightweight** tag is very much like a branch that doesn’t change — it’s just a pointer to a specific commit.

**Annotated** tags, however, are stored as full objects in the Git database. They’re checksummed; contain the tagger name, email, and date; have a tagging message; and can be signed and verified with GNU Privacy Guard (GPG). It’s generally recommended that you create annotated tags so you can have all this information; but if you want a temporary tag or for some reason don’t want to keep the other information, lightweight tags are available too.

##### Annotated Tags

By specify `-a`, such as `git tag -a v1.1 -m "my version 1.1"`

You could see the tag data along with the cmmit that was tagged by using the `git show` command, such as `git show v1.1`

##### Lightweight Tags

`git tag <tagname> ` which is the commit checksum stored in a file -- no other information is kept.

#### Tagging Later

Suppose you forgot to tag the project at v1.2. You could find the commit checksum (or part of it) by using `git log`, then `git tag -a v1.1 checksum` .

#### Sharing Tags

By default, the `git push` command doesn't transfer tags to remote servers. You need to explicitly push tags to a shared server after creating them. 

Run `git push origin <tagname>`.

If you have a lot of tags that you want to push up at once, just running `git push origin --tags`.

#### Deleting Tags

To delete a tag on your local repository, you can use `git tag -d <tagname> `.

**Attention!** It does not mean that tagname was removed from any remoted servers. There are two ways to tackle with.

1. `git push <remote> :refs/tags/<tagname>`, such as `git push origin :refs/tags/v1.1`.The way to interpret the above is to read it as the null value before the colon is being pushed to the remote tag name, effectively deleting it. 
2. `git push origin --delete <tagname>`

### Git Aliases

`git config --global alias.<alias> <original name> `



