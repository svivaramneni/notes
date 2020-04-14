### VCS
* Git is a distributed version control system.
* CVS maintains versions at file level and SVN does it at folder level. Both work on the model of central repositories.
* Change sets is the key.
### Git Configurations
* System -> etc/gitconfig -> git config --system
* User -> ~/.gitconfig -> git config --global
* Project -> my_project/.git/config -> git config

### Common Git workflow
* Make changes
* Add the changes
* Commit changes with a message.

### Commit Message best practices
* A short single-line summary < 50 chars
* Optionally followed by a blank line and a more complete description.
* Keep eachline less than 72 chars
* Use present tense. Ex: Fix for a bug

### View log messages
* git help log
* git log -n 5
* git log --grep="transaction"

### Git has 3 stages
* repository - git commit
* staging index - git add abc.java
* working directory

### Viewing Diff
* git diff
* git diff --staged -> For viewing difference between repository and staged 
* git diff 1c11694..9dcff6e_--color-words -> To view diff b/w 2 commits

### Undo Changes
* git checkout -- a.java -> reverts unstaged files.
* git commit --amed -m "commit message" -> Modifies most recent commit.
* git revert a84791uqiu893 - Revert a commit
* git clean -n


### Popular Commands
* Help command
'git help log'



* List all configurations
git config --list

git add -A -> moves all files to staging area
git reset ABC.java -> resets files from staging area.
git commit -m "Initial Commit"
git log
git clone "remote url" .
git branch -a
git diff
git pull origin master
git push origin master
git show ab1234def - Display changes in one commit.

workflow

git branch sridhar-v/LRN
git checkout sridhar_v/LRN
git branch
make changes
commit and push.
git push -u origin master
git checkout master
git merge substract
