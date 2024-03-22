# Local and Global GIT variables
 
  Why is this so important? Adding a user.name to git config --global means
	there is another user.name present if the file is not empty. The lack of
	error checking and UI warning messages make this error prone. 
  
  1) format: section.key git config --add --global user.name "bob" adds bob to the variable user.name. User is a section in .git/config and name is a entry in the section.
  2) operations: --add --list --get-regexp --unset --unset-all
  3) locations: --global and --local each section.key can have multiple destinations, global, local and --file.

  Note the below dangerous inconsistency: 
  - a cat of .git/config shows user.name=foo
  ➜  git_demos git:(trunk) ✗ cat .git/config
[core]
        repositoryformatversion = 0
        filemode = true
        bare = false
        logallrefupdates = true
        ignorecase = true
        precomposeunicode = true
[user]
        :star: name = foo :star:
  - git config --local --get user.name >foo 
  - git config --global --get user.name > doug chang
  - git config --get user.name >foo
  
  Very confusing to determine which value the runtime is using when. There are also other sources in git_install/etc/gitconfig which you cant access wo sudo. list with --show-scope and --show-origin. These flags don't fix anything. They don't warn you if the runtime is taking values from unexpected locations. 
