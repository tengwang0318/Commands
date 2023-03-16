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

[the life cycle of the status of your files](pic/1.png)





























