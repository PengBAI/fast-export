# Mercurial to Git migration guide!
[![Docker Hub](https://img.shields.io/badge/docker-ready-blue.svg)](https://hub.docker.com/r/pengbai/docker-mercurial2git/)

Thanks for the contribution of Arnaud ADAM and the original project frej/fast-export.

Here is a migration guide to help you with! :smile:

In your WORKSPACE, create a subdirectory named *m2g*, and in this subdirectory,
checkout your mercurial repository into a directory (the name doesn't matter, it will be *my-hg-project* here),
create an empty directory (which will contain you git project sources). for this example, I'll take *my-git-project*.

* launch your docker container with following command,

```Bash
$ docker run -it --rm -v WORKSPACE/m2g:/home/m2g pengbai/docker-mercurial2git
```
* go to your empy git directory, and init the repository,

```Bash
$ cd m2g/my-git-project
$ git init
Initialized empty Git repository in /home/m2g/my-git-project/.git/
```
* then execute fast-export script as follows,

```Bash
$ /home/fast-export/hg-fast-export.sh -r ../my-hg-project
```
In theory, you'll see a bunch of logs on your screen. Migration can take a while...
* finally, do a checkout of your new git project,

```Bash
$ git checkout HEAD
```
* add your remote repository url (replace following url with the real one!),

```Bash
$ git remote add origin https://github.com/xxxx/my-git-project.git
```
* and push all your project to your new git repository!

```Bash
$ git push origin --all
```
 
That's all! :sunglasses:
You're now able to work with your 'git' project.

You can now exit your docker container, and delete the m2g folder (since you're now able to clone your repository anywhere you want!).

Please note that :
* the 'default' branch in Mercurial will be the 'master' one in Git...
* Git doesn't like spaces very much...it means that if you had some branches or tags with spaces into the name, Git will replace it with underscore.
* Branch with multiple heads isn't allowed. If you closed a branch, and reopen a new one with same name, migration doesn't work.
 
Have fun! :+1:
