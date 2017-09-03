Git cheatsheet
==============

All behaviour tested and documented with git 2.12 - 2.14.



Table of Contents
-----------------
  
» [Repositories](#repositories)  
» [Submodules](#submodules)  
» [Commits](#commits)  
» [Stashes](#stashes)  
» [Branches](#branches)  
» [Tags](#tags)  
» [Merging and Rebasing](#merging-and-rebasing)  
» [Remotes](#remotes)  
» [Fetching and Pushing](#fetching-and-pushing)  
» [Reporting](#reporting)  
» [Configuration](#configuration)  



Repositories
------------

To create a new git repository and check out a new branch named `master`:

```
git init                                 # At current path.
git init <path>                          # At <path>.
git init --bare                          # Repository without a working tree.
```

To get a copy of an existing repository, add a remote for `<path>` named `origin`, create remote-tracking branches, and check out the one tracking `HEAD` on the remote:

```
git clone <path>                         # Clone under the same name.
git clone <path> <name>                  # Clone under a different name.
git clone --bare <path>                  # Clone as bare. By convention, their names end in `.git`.
git clone --origin <remote> <path>       # Name the remote <remote> instead of `origin`.
git clone --recursive <path>             # Clone, initialise and update submodules.
```



Submodules
----------
 
To show the status of submodules:

```
git submodule status                     # Print the commit SHA1, submodule path, and `git describe` of SHA1.
```

To add, initialise and update submodules:

```
git submodule add <path>                 # Add entries to `.gitmodules` and `.git/config` for <path> and clone it.
git submodule add <path> <name>          # Add and clone under <name>.
```
```
git submodule init                       # Add entries to `.git/config` for submodules listed in `.gitmodules`.
git submodule init <path> …              # Init submodule at <path>.
```
```
git submodule update                     # Fetch and check out all submodules to their commits.
git submodule update <path> …            # Update submodule at <path>.
git submodule update --init              # Init and update submodules.
```

To rename a submodule:

```
git mv <old> <new>                       # Rename the submodule's directory and its path in `.gitmodules`.
```

To remove a submodule:

```
git submodule deinit <path> …            # Remove the entry from `.git/config` and clear the <path> directory.
git rm -f <path>                         # Remove the entry from `.gitmodules` and remove the <path> directory.
rm -rf .git/modules/<path>               # Remove the submodule's .git directory from `.git/modules/`.
```



Commits
-------

To show the checked out and all preceding commits (see [Reporting](#reporting) for more options):

```
git log
```

To add, rename and remove files or directories to and from the index and working tree:

```
git add <path> …                         # Stage file at <path>.
git add -p <path>                        # Stage parts of <path> interactively.
```
```
git mv <old> <new>                       # Rename a file in the index and working tree.
```
```
git rm <path> …                          # Remove from index and working tree if no data is lost.
git rm -f <path>                         # Remove from index and working tree.
git rm --cached <path>                   # Remove from index.
git rm -r <path>                         # Remove recursively.
```

To store the contents of index in a new commit and make the checked out branch point to it:

```
git commit                               # Type the message in your editor.
git commit -m "message"                  # Type the message inline.
git commit --amend                       # Overwrite previous commit.
git commit <file> …                      # Commit <file> without the index.
```

To make a new commit by applying changes introduced with `<commit>`:

```
git cherry-pick <commit>                 # Requires a clean working tree.
```

To make a new commit undoing the changes made since `<commit>`:

```
git revert <commit>
git revert -m <n> <commit>               # Choose the <n>-th parent of <commit>, discarding all other changes.
```

To revert specific files to their state in `<commit>`:

```
git reset <commit> <file>                # Revert in index.
git checkout <commit> <file>             # Revert in working tree.
```

To remove untracked files from the working tree:

```
git clean -f                             # Delete untracked files.
git clean -d                             # Delete untracked files and directories.
git clean -x                             # Delete untracked and ignored files.
git clean -i                             # Clean interactively.
git clean --dry-run                      # Show which files would be deleted.
```



Stashes
-------

To list and inspect stored stashes:

```
git stash list
```
```
git stash show <n>                       # Show diff between the <n>-th stash and the commit when it was stashed.
```

To store changed files in index and working tree and check out `HEAD`:

```
git stash                                # Stash tracked files.
git stash -u                             # Stash tracked and untracked files.
git stash -a                             # Stash tracked, untracked and ignored files.
git stash "message"                      # Add a message to the stash.
git stash --keep-index                   # Don't clear the index.
```

To re-apply a stash to the working tree:

```
git stash apply                          # Apply the latest stash.
git stash apply <n>                      # Apply the <n>-th stash.
git stash apply --index                  # Apply changes to the index too.
```

To delete a stash:

```
git stash drop <n>                       # Drop the <n>-th stash.
git stash pop <n>                        # Apply and drop the <n>-th stash.
git stash branch <name> <n>              # Check out a new branch at the commit of the <n>-th stash and pop it.
git stash clear                          # Drop all stashes.
```



Branches
--------

To list branches:

```
git branch                               # List local branches.
git branch -r                            # List remote branches.
git branch -a                            # List local and remote branches.
git branch -vv                           # List branches and their upstream branches, along with their commits.
git branch --merged <commit>             # List branches reachable from <commit>, defaulting to HEAD.
git branch --no-merged <commit>          # List branches not reachable from <commit>, defaulting to HEAD.
```

To create, rename and remove branches:

```
git branch <name>                        # Create a new branch pointing to HEAD.
git branch <name> <commit>               # Create a new branch pointing to <commit>.
```
```
git branch -m <new>                      # Rename checked out branch.
git branch -m <old> <new>                # Rename specified branch.
```
```
git branch -d <branch>                   # Delete a branch.
git branch -dr <remote/branch>           # Delete a remote-tracking branch.
```

To add and remove an upstream branch:

```
git branch -u <remote/branch> <branch>   # Make <branch> (defaulting to HEAD) track <remote/branch>.
git branch --unset-upstream <branch>     # Stop <branch> (defaulting to HEAD) from tracking the upstream branch.
```

To make the checked out branch point to `<commit>`:

```
git reset --soft <commit>                # Leave the index and working tree intact.
git reset --mixed <commit>               # Update the index, leaving the working tree intact. Default.
git reset --hard <commit>                # Update the index and working tree, overwriting local changes.

git branch -f <branch> <commit>          # Make <branch> point to <commit>.
```

To make `HEAD` point to `<branch>` and update the index and working tree to match it, failing if any data would be lost:

```
git checkout <branch>
git checkout -b <branch>                 # Create a new <branch> and check it out.
git checkout -b <branch> <remote/branch> # Create a new <branch> that tracks <remote/branch> and check it out.
git checkout --orphan <branch>           # Create a new <branch> without parents and check it out.
```



Tags
----

To list tags:

```
git tag
git tag -l <pattern>                     # List tags containing the glob <pattern>.
```

To create a tag:

```
git tag <name>                           # Lightweight tag pointing to HEAD.
git tag <name> <commit>                  # Lightweight tag pointing to <commit>.
git tag <name> -a                        # Annotated tag.
git tag <name> -m "message"              # Annotated tag with the message inline.
```

To delete a tag:

```
git tag -d <name>
```



Merging and Rebasing
--------------------

To merge `<branch>` into the checked out branch, introducing a new commit unless fast-forwarding:

```
git merge <branch>
git merge --squash <branch>              # Populate the index without committing.
```

To reset the checked out branch to `<branch>`, apply differences between `HEAD` and the common ancestor, and commit:

```
git rebase <branch>                      # Reset HEAD to <branch>.
git rebase <branch1> <branch2>           # Reset <branch2> to <branch1>.
git rebase --onto <branch1> <branch2>    # Reset HEAD to <branch1>, applying HEAD to <branch2> differences.
```

To rebase interactively, starting with the commit following `<commit>`:

```
git rebase -i <commit>
git rebase -i --root                     # Start from the first commit.
```



Remotes
-------

To list and inspect remotes:

```
git remote
git remote -v                            # Include fetch/push urls.
```
```
git remote show <remote>                 # Show fetch/push urls, list remote and their downstream branches.
```

To add, rename or remove a remote:

```
git remote add <remote> <path>
```
```
git remote rename <old> <new>
```
```
git remote remove <name>
```

To list references of a remote repository without fetching:

```
git ls-remote <remote>                   # List branches and tags.
```



Fetching and Pushing
--------------------

To download new data on `<branch>` from `<remote>` and update the remote-tracking branch:

```
git fetch <remote> <branch>              # Fetch <branch> from <remote>.
git fetch <remote>                       # Fetch all branches from <remote>.
git fetch                                # Fetch from the remote of the upstream branch, or `origin`.
git fetch --prune                        # Fetch and remove dead remote-tracking branches.
git fetch --recurse-submodules           # Fetch submodules.
git fetch --all                          # Fetch from all remotes.
```

To fetch (with same options) and merge `<remote/branch>` into the checked out branch:

```
git pull <remote> <branch>
git pull                                 # Pull from the upstream branch.
git pull --rebase                        # Fetch and rebase.
```

To send new commits on `<branch1>` to `<branch2>` on `<remote>`, creating a new branch if it does not exist:

```
git push <remote> <branch1>:<branch2>
git push <remote> <branch>               # Push <branch> to <branch> on <remote>.
git push                                 # Push the checked out branch to its upstream branch.
git push -u                              # Push and make the pushed branch track the remote one.
git push -f                              # Push even if the remote branch is not an ancestor of the pushed one.
git push --dry-run                       # Show what would be pushed.
git push --all                           # Push all branches.
git push --tags                          # Push all tags.
```

To delete `<branch>` on `<remote>`:

```
git push -d <remote> <branch>
```



Reporting
---------

To open the manual page for `<topic>`:

```
git help <topic>
```

To show tags (message and referenced object), commits (message and diff), blobs (plain contents) or trees (names):

```
git show <object>
```

To show the checked out branch and its relation to the upstream branch, and to list files that changed in index or working tree:

```
git status
git status <path>                        # Show status of files at <path>.
git status -s                            # Show status compactly.
git status -u                            # List individual untracked files, not directories.
```

To list staged files:

```
git ls-files
git ls-files -s                          # List staged files along with mode bits, object name and stage number.
git ls-files -u                          # List unsuccessfully merged files.
```

To show what was changed but not yet staged in tracked files:

```
git diff                                 # All tracked files.
git diff <path>                          # Tracked files at <path>.
git diff --cached                        # Show what was staged but not yet commited.
git diff --submodule                     # Show differences in submodules.
git diff <ref1> <ref2>                   # Show differences between <ref1> and <ref2>.
git difftool                             # Use an external diff tool, with the same options and arguments.
```

To show commit, author and date of the last modification for each line of `<file>`:

```
git blame <file>
```

To show commit logs:

```
git log                                  # Show commits preceding and including the checked one.
git log <commit1>..<commit2>             # Show commits reachable by <commit2> that aren't reachable by <commit1>.
git log <commit1>...<commit2>            # Show commits reachable by either but not both.

git log --all                            # Include all branches.
git log --graph                          # Show an ASCII representation of branches and merges.
git log --decorate                       # Show branches and tags next to commits.
git log --stat                           # Show an overview of file edits in each commit.
git log --abbrev-commit                  # Show checksums in short form.
git log --relative-date                  # Show dates in format relative to now.
git log --pretty=format:"<pattern>"      # Use a custom format, see `git help log` for details.

git log <path>                           # Show commits that introduced a change to files at <path>.
git log -<n>                             # Show the last <n> entries.
git log --after=<date>                   # Show commits created after the date (in absolute or relative form).
git log --before=<date>                  # Show commits created before the date (in absolute or relative form).
git log --author=<name>                  # Show commits whose author is <name>.
git log --committer=<name>               # Show commits whose committer is <name>.
git log --grep <regex>                   # Show commits whose message matches <regex>.
git log -S <string>                      # Show commits that add or remove <string>.
git log -G <regex>                       # Show commits that add or remove lines that match <regex>.
git log --all-match                      # Match all filters, not any.
```

To show the local history of `HEAD`'s tip updates:

```
git reflog                               # Alias for `git log --walk-reflogs --abbrev-commit --pretty=oneline`.
git reflog <branch>                      # Show <branch>'s reflog.
```
 
To return the corresponding SHA-1 string of `<object>`:

```
git rev-parse <object>
```



Configuration
-------------

To list configured options from all config files:

```
git config -l
git config -l --name-only                # Exclude values.
git config -l --show-origin              # Include file paths.
```

To get, set or unset the value of an option of a specific config file (defaulting to `--local`):

```
git config <option>                      # Get.
```

```
git config <option> <value>              # Set.
```

```
git config --unset <option>              # Unset.
```

To use a specific config file:

```
git config --local                       # Use `.git/config`.
git config --global                      # Use `~/.gitconfig`.
git config --system                      # Use `/etc/gitconfig`.
```
