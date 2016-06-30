# GITTE - GIT CHEAT SHEET

##### Commands marked with '=>' are aliases. See .gitconfig file for details.

##### Useful commands
```
=> git alias
git [command] --help                     // display help for specified command
```

-------------------

##### Create a repository
```
git init                               // init empty repository
git clone [remoteRepo] [localDir]      // clone git repo to local directory
=> git makegitrepo                     // create git repo, add README.md file and make initial commit
```

-------------------

##### Observe your repository
```
=> git s                                       // git status
=> git st                                      // git status -sb
git diff                                       // show changes to files not yet staged
=> git difff                                   // highlight changed words using only colors (without plus and minus)
git diff HEAD                                  // show all staged and unstaged changes
git diff commit1 commit2                       // show the changes between two commits ids
git diff <branch name>                         // show the changes regarding other branch
git diff --stat [firstBranch] <secondBranch>   // compare two branches based on statistics
git blame                                      // annotate the file
git log                                        // show full change history
git log -p [file/directory]                    // show change history for file/direcotyr including diffs
=> git llog                                    // show pretty list of lat 25 commits (id, timestamp, user, message)
=> git ltree                                   // show pretty graph from logs
=> git hist                                    // show pretty graph with history
=> git histfull                                // show pretty graph with history + changed files
=> git changelog                               // show commit messages list
=> git changelogextended                       // show commit messages list with date, author, etc.
=> git days                                    // dates of commits
=> git rp                                      // rev-parse --short=4
=> git find [name]                             // finds a filename in the git repository, gives absolute location
```

------------------

##### Make a change :
```
git add [file]                                  // stage a file with given filename
git add .                                       // stage all changed files, ready for commit
=> git co -m "Commit message"                   // commit staged files
=> git save Commit message                      // stage and commit files with message
=> git amend Commit message                     // make stage & commit with amend
git reset [file]                                // unstages file, keeping the changes
git checkout -- [filename]                      // undo specific file if unstaged
git reset --hard                                // revert everything to the last commit
git revert [commit]                             // generate a new commit that undoes all of the changes introduced in [commit]
=> git unstage                                  // remove everything what was prepared for commit (git reset HEAD --)
```

-------------------
##### Stash
```
git stash list                                   // show stashes
git stash                                        // save stash
git stash apply                                  // get the changes from top/last stash
git stash apply [id]                             // get the changes from specified stash
git stash drop                                   // clear stash
=> git sta                                       // stash with untracked files too
```

-------------------

##### Working with branches
```
=> git br                                          // git branch
git branch                                         // list all local branches
git branch -r                                      // list of remote branches
=> git bbranch                                     // extended info about local branches
=> git branches                                    // detailed info about local and remote branches
=> git ch                                          // git checkout
git checkout [branch]                              // switch to specific branch / for never version of Git get remote branch+tracking
git checkout -b [branch] origin/[branch]           // for older version of Git checkout remote branch
git checkout -b [branch]                           // create and switch to new branch
git branch [branch]                                // create new local branch with given name
git branch -d [branch]                             // delete branch with given name
git merge [branch]                                 // merge to actual branch from given branch name
git checkout [branchB] && git merge [branchA]      // merge branchA into branchB
git merge --no-ff [branch]                         // merge to actual branch without fast forward
=> git mergenoff [branch]                          // merge to actual branch without fast forward
git merge [branch] --no-commit --no-ff             // merge to actual branch without fast forward and auto commit
```

-------------------

##### Synchronize
```
git fetch                                          // get the latest changes from origin (no merge)
git pull                                           // fetch the latest changes from origin and merge
=> git purr                                        // fetch the latest changes from origin and rebase (pull --rebase)
=> git puff                                        // pull with fast forward only (pull --ff-only)
git remote                                         // check defined remote repositories
git remote add origin [remoteRepo]                 // add remote repository
git push -u origin [branch]                        // push given branch to origin remote repo with tracking
=> git publish                                     // pushes the current branch to the origin (or different repo if is provided as param)
=> git unpublish                                   // deletes the remote version of current branch in origin (or different repo if provided as param)
git push origin --delete [branch]                  // delete remote branch
=> git trackallbranches                            // get all remote branches
=> git updateallbranches                           // pull (update) all remote branches
=> git showorigin                                  // display the branches on origin, who modified, when, etc. useful for gitflow
```

-------------------

##### Tags
```
git tag                                             // list of tags
=> git tags                                         // display tags with hashes
git tag -d [tagName]                                // delete the tag with specified name
git tag [tagName]                                   // tag the current commit
git tag -a [tagName] -m ["Tag message"]             // create new tag with message
git tag [tagName] [commitID]                        // use tagging to mark a significant changeset, such as a release
git push --tags origin                              // push all tags to remote repository
=> git pushtags                                     // push all tags (push --tags)
=> git tagwithdate [prefix]                         // create tag with prefix and date (PREFIX_12-01-12_15-25-25)
=> git lasttag                                      // display last tag
=> git checkoutlasttag                              // checkout the last tag
=> git publishtag [tagName] [repo | null]           // pushes given tag to remote repo (or origin if repo is not provided)
=> git unpublishtag [tagName] [repo | null]         // removes given tag from remote repo (or origin if repo is not provided)
```

-------------------

##### Basic repo information / what was going on while you were away
```
=> git stat                              // repository statistics
=> git whois                             // display the user information
=> git whatis [branch/tag/name]          // telling us what was the last commit in specified branch/tag/name 
=> git howmany                           // display the number of commits
=> git howmanybywhom                     // group number of commits by users
=> git anychanges [branch]               // do we have any changes on origin for specified branch
=> git anychangesonmaster                // do we have any changes on origin/master
=> git whoischanging [branch]            // who does introduce the changes on the specified branch from last pull
=> git whoischangingmaster               // who does introduce the change on master from last pull
```

-------------------

# TIPS & TRICKS

##### Rebasing new branch instead of merging
```
git checkout experiment                // switch to that branch
git rebase master                      // rebase it to selected branch, in this case move it on the top of the master
```
-------------------

##### Git Rebase For Linear History
```
git commit
git pull
git rebase -i origin/master
git push origin master
```

--------------------------

##### Modify specified commit

You can use git rebase, for example, if you want to modify back to commit bbc643cd, run

	$ git rebase --interactive bbc643cd^

In the default editor, modify 'pick' to 'edit' in the line whose commit you want to modify. Make your changes and then stage them with

	$ git add <filepattern>

Now you can use

	$ git commit --amend

to modify the commit, and after that

	$ git rebase --continue

--------------------------

##### UPDATE FORK

1. Add the remote, call it "upstream":  
```git remote add upstream https://github.com/whoever/whatever.git```
2. Fetch all the branches of that remote into remote-tracking branches, such as upstream/master:   
```git fetch upstream```
3. Make sure that you're on your master branch:   
```git checkout master```
4. Rewrite your master branch so that any commits of yours that aren't already in upstream/master are replayed on top of that other branch:   
```git rebase upstream/master && git push -f origin master```

So everything looks like:
```
git remote add upstream https://github.com/whoever/whatever.git
git fetch upstream
git checkout master // no needed if you are on master
git rebase upstream/master 
git push -f origin master
```

There is a special alias ```updatefork``` in order to fetch upstream, checkout master, rebase and push to our origin repo.

### Sources:

- https://github.com/jakubnabrdalik/gitkurwa (see there the links to source of that great set of aliases)
- http://helion.pl/ksiazki/git-rozproszony-system-kontroli-wersji-wlodzimierz-gajda,gitroz.htm
- ZeroTurnaround Git Cheat Sheet
- StackOverflow :)


### Feel free to create pull request!
