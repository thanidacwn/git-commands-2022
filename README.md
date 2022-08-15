## Using Git

<!-- > TODO: Create a table of contents here.  Each line should be a clickable link to each part of this document or another file containing the questions and answers. One item per line. -->

| content       |                                                   
| ------------- |                                                     
| [Basics](#basics)|   
| [Adding and Changing Things](#adding-and-changing-things)|          
| [Undo Changes and Recover Files](#Undo-Changes-and-Recover-Files)|   
| [Branch and Merge](#branch-and-merge)|
| [Viewing Commits](#viewing-commits)|
| [Favorites](#favorites)|
| [Resources](#resources)|

#### Note on Paths

In this file, directory paths are written with a forward slash as on MacOS, Linux, and the Windows-Bash shell: `/dir1/dir2/somefile`.    


## Basics

1. When using Git locally, what are these?  Define each one in a sentence
   * Staging area - ```files that are going to be a part of the next commit```
   * Working copy -  ```or call 'working directory' repesent files that you clone your github repository```
   * master -  ```defult branch of git```
   * HEAD - ```refer to active or current branch```

2. When you install git on a new machine (or in a new user account) you should perform these 2 git commands to tell git your name and email.  These values are used in commits that you make:
   ```
   # Git configuration commands for a new account
      git config --global user.name "THANIDA CHAIWONGNON"
      git config --global user.email "thanida.chai@ku.th"
   ```

3. There are 2 ways to create a local Git repository.  What are they?


   - **First way** : take a local directory that is currently not under version control, and turn it into a Git repository

   - **Second way**: clone an existing Git repository from elsewhere.


4. When you create a git repository by entering `git init`, Git will create a "hidden" directory for the local repository.  Where is the directory for this local repository (relative to the directory where you typed "git init")?

   
      : Files are contained in the **.git** directory that created. Enter ```git add``` commands that specify the files want to track and followed by ```git commit``` then the directory is wherever your files are on your local.
   


## Adding and Changing Things

Suppose your working copy of a repository contains these files and directories:
```
README.md
out/
    a.exe
src/a.py
    b.py
    c.py
test/
    test_a.py
    ...
```     
<!-- > TODO: Write the git command to perform each of these: -->

1. Add README.md and *everything* in the `src` directory to the git staging area.
   ```
   git add README.md
   git commit
   git add src
   git commit
   ```

2. Add `test/test_a.py` to the staging area (but not any other files).
   ```
   git add test
   git commit
   ```

3. List the files in the staging area.
   ```
   git status
   ```


4. Remove `README.md` from the staging area. (Useful if you accidentally add something you don't want to commit.)

   ```
   git reset HEAD README.md
   ```


5. Commit everything in the staging area to the repository.

   ```
   git commit 
   ```


6. Describe 2 steps to configure the repository so git will ignore all files in the `out/` directory:
   - step one : Create a file listing patterns to match them named ```.gitignore``` and blank lines or lines starting with '#' are ignored \
               ```# ignore all files in any directory named 'out'```

   - step two : Use a forward slash (/) to specify a directory.\
               ```out/```


7. Command to move all the .py files from `src` to the top-level directory of this repository, so they are also moved in the Git repo.
   ```
   git mv src/*.py .
   ```

8. Commit this change with the message "moved src directory":
   ```
   git commit -m "moved src directory"
   ```


9. Command to add **all changed files** (but not untracked files) to the staging area using a single command.

   ```
   git add -u
   ```


10. **Delete** the file `c.py` from your working copy **and** the repository:

      ```
      git rm c.py
      ```


## Undo Changes and Recover Files

<!-- > TODO: enter the git command to do each of these -->

1.  Display the differences between your *working copy* of `a.py` and the `a.py` in the *local repository* (HEAD revision):

      ```
      git diff HEAD a.py
      ```


2. Display the differences between your *working copy* of `a.py` and the version in the *staging area*. (But, if a.py is not in the staging area this will compare working copy to HEAD revision):

      ```
      git diff --cached
      ```

3. **View changes to be committed:** Display the differences between files in the staging area and the versions in the repository. (You can also specify a file name to compare just one file.) 

   ```
   git diff --staged
   ```


4. **Undo "git add":** If `main.py` has been added to the staging area (`git add main.py`), remove it from the staging area:
   ```
   git reset HEAD main.py
   ```

5. **Recover a file:** Command to replace your working copy of `a.py` with the most recent (HEAD) version in the repository.  This also works if you have deleted your working copy of this file.

   ```
   git restore HEAD a.py
   ```


6. **Undo a commit:** Suppose you want to discard some commit(s) and move both HEAD and "master" to an earlier revision (an earlier commit)  Suppose the git commit graph looks like this (`aaaa`, etc, are the commit ids)
   ```
   aaaa ---> bbbb ---> cccc ---> dddd [HEAD -> master]
   
   git reset --hard bbbb
   ```
   The command to reset HEAD and master to the commit id `bbbb`:


7. **Checkout old code:** Using the above example, the command to replace your working copy with the files from commit with id `aaaa`:
   ```
   git checkout aaaa
   git clean -d -n
   ```
    Note:
    - Git won't let you do this if you have uncommitted changes to any "tracked" files.
    - Untracked files are ignored, so after doing this command they will still be in your working copy.
 

## Viewing Commits

1. Show the history of commits, using one line per commit:
   ```
   git log --oneline
   ```
   Some versions of git have an *alias* "log1" for this (`git log1`).

2. Show the history (as above) including *all* branches in the repository and include a graph connecting the commits:

   ```
   git log --all --graph
   ```


3. List all the files in the current branch of the repository:
   ```
   git ls-files
   ```
   example output:
   ```
   .gitignore
   README.md
   a.py
   b.py
   test/test_a.py
   test/test_b.py
   ```


## Branch and Merge

<!-- > TODO write the commands to do each of these -->
1. Create a new branch named `dev-foo`:
   ```
   git branch dev-foo
   ```
 
2. Display the name of your current branch:
   ```
   git branch –show-current
   ```

3. List the names of **all** branches, including remote branches:

   ```
   git branch -a
   ```

4. Switch your working copy to the branch named `dev-foo`:

   ```
   git checkout dev-foo
   ```

5. **Merge:** To merge the work from `dev-foo` into the master branch, perform these steps:
   <!-- > TODO: write a description of the steps and the git command(s) for each step -->
   1. step one : check ```git status``` and check out the branch that want to merge
      ```
      git status
      git checkout master
      ```
   2. step two : merge dev-foo branch into the master branch
      ```
      git merge dev-foo
      ```

6. Describe under what conditions a merge may fail.
      ```

      : Sometime when we starting merge may fail because if Git knows there are changes in your working directory that could be written over by the files that you are merging in. there are no merge conflicts in individual files or Git can fail during the merge because when we committed changes that are in conflict with someone else's committed changes. Git will do it best to merge the files and will leave things for you to resolve manually in the files it lists.
      
      ```


## Favorites

   **git status** : to display the state of the working directory and the staging area and see which changes have been staged, which haven't, and which files aren't being tracked. ```git status``` it's easy to remember and use often.



---
## Resources

[noble desktop](https://www.nobledesktop.com/learn/git) Git Tips & Commands\
[Pro Git Online Book][ProGit] Chapters 2 & 3 contain the essentials. Downloadable PDF is also available.     
[Visual Git Reference](https://marklodato.github.io/visual-git-guide) one page with illustrations of git commands.

Try Git:

[Learn Git Interactive Tutorial][LearnGitInteractive] excellent visual tutorial.   
[Git Visualizer][VisualizeGit] execute Git commands in a web browser and see the results as a graph.    

[ProGit]: https://www.git-scm.com/book/en/v2 "Pro Git online book on Git-scm.com"
[ProGitPdf]: https://progit2.s3.amazonaws.com/en/2016-03-22-f3531/progit-en.1084.pdf "Pro Git v.2 PDF on AWS. Longer, book format."
[LearnGitInteractive]: https://learngitbranching.js.org "Interactive graphical git tutorial"
[VisualizeGit]: http://git-school.github.io/visualizing-git/ "Online tools draws a graph of commits in a repo as you type"
[markdown-cheatsheet]: https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet
[github-markdown]: https://docs.github.com/en/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax
[vscode-markdown-preview-enhanced]: https://marketplace.visualstudio.com/items?itemName=shd101wyy.markdown-preview-enhanced
