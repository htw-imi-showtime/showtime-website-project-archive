# git submodule showtime-project-archive

This submodule contains all projects from former terms no longer
contained in the showtime website repo.

It has been extracted as a submodule as project teams
don't need to download all former projects (include it)
in order to create their own sites.

# If you want to add or change it

Get the submodule: (if you haven't cloned the repository 
yet, just add `--recurse-submodules` parameter to clone command)

    git submodule update --init project-archive

This populates the folder ./project-archive with a 
clone of the project archive ([https://github.com/htw-imi-showtime/showtime-website-project-archive](https://github.com/htw-imi-showtime/showtime-website-project-archive))

### Moving terms to the archive



## The Mechanics

git stores the information about the submodule in two places:

1. .gitmodules file:

    `cat .gitmodules`
    ```
    [submodule "archive"]
    	path = project-archive
    	url = ../../htw-imi-showtime/showtime-website-project-archive.git
    	branch = main
    ```
2. the associated commit in the repo:

    `cat .git/modules/archive/HEAD`
    ```
        720531a76d6aa718f3e4c0797bd08491e5fdac25
    ```
Thus, if you change the submodule and create a new commit, this reference needs to be updated to this new commit.

`git status`

    ...
	modified:   project-archive (new commits)
    ...

you get specific information with 

`git diff``
```
diff --git a/project-archive b/project-archive
[core]
        repositoryformatversion = 0
index 9a86b17..720531a 160000
--- a/project-archive
+++ b/project-archive
@@ -1 +1 @@
-Subproject commit 9a86b17ae80a5222962395d503921e4efe61e636
+Subproject commit 720531a76d6aa718f3e4c0797bd08491e5fdac25
```

This change can be added, committed and pushed (!) just like any other change.

## Reducing Submodule Clone Depth:

** tl;dr: not worth the hassle **

It is also possible to clone the repo directly into the project-archive subdirectory (delete it first), which makes it possible to use the --depth 1 parameter:

    git clone --depth 1 git@github.com:htw-imi-showtime/showtime-website-project-archive.git project-archive

up to ss23 this only made a difference of roundabout 200 git objects - 

 - all commits: Receiving objects: 100% (1869/1869)
 - depth 1: Receiving objects: 100% (1697/1697)

which makes sense as the there are many little files, and only some of them 
are changed 2-3 times max altogether.

## Links

Working with submodules may be a bit confusing at start. 


"Submodules allow you to keep a Git repository as a subdirectory of another Git repository. This lets you clone another repository into your project and keep your commits separate."

- git submodule documentation https://git-scm.com/book/en/v2/Git-Tools-Submodules
