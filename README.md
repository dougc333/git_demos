# Git Notes

Where I wasted hours debugging because of false assumptions in Git.  

## Setting Config variables

Innocous enough. Hundreds-Thousands of wasted hours. The config variable values propagate into the repo and are virtually impossible to fix without extensive manual labor. 

There are several disguised hidden "features" for config variables. 

- There are multiple locations for what is asumed to be a global variable AND multiple values in the same location. 
  - global
  - local
  - worktree
  - system
  - file which specifies the path for the .git/config file in each of the above namespaces
  A user name can have many values even though the OBVIOUS "getter" command only lists one.
  git config --get user.name > bugs bunny. Cannot assume "bugs bunny" is user.name. There can be multiple names for user.name. Hundreds to thousands of hours spent fixing user.name for repos when users inadvertently didn't notice their user name was not what they thought it would be.

Git --global, --local variables are set using git config --add section.var "hi" where section is init and var is

  - init.defaultBranchName
  The default branchName changes from Master to Main or your own convention.
git config --add user.name "bob"
git config --add user.email "asd@asd.cs"

git config --global init.defaultBranchName "trunk"

Be careful. These are key:value where key is section.var and value is an array.
Running git config --add user.email "asdf" will add user.email to the existing
user.email. It does NOT overwrite the existing value and replace.

cat .git/config to list all config variables

q) Is git remote add and git push --set-upstream a .git/config variable? It looks like it with the add but
it doesnt match the git config --add format exactly.

git remote add origin https://github.com/OWNER/REPOSITORY.git
git push --set-upstream origin trunk

## Merging and Fixing Trees

10-100x wasted time compared to config vars. Wasted some multiple of thousands of hours. Most call this branch and merge, this repo focuses on merge and fix. Fix = modify tree shape.  

- The merge commit messages pollute the history. What to do?
- Fixing a messed up merge.
- Fixing trees in a shape which is not the desired shape.

How to present a single commit to a group project. How to fix merges and messed up branches, ie moving files between branches.  
