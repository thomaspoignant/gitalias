# gitalias
Some alias very useful

## Install the alias

To install just run this command line and it will add all these aliases to your `.gitconfig` file.

```sh
git clone https://github.com/thomaspoignant/gitalias.git && echo -e "[include]\n   path = $(pwd)/gitalias/.gitalias\n$(cat ~/.gitconfig)" > ~/.gitconfig
```

## aliases

```properties
[alias]
  #print log 
  ls = log --pretty=format:"%C(yellow)%h%Cred%d\\ %Creset%s%Cgreen\\ [%cn]" --decorate
  ll = log --pretty=format:"%C(yellow)%h%Cred%d\\ %Creset%s%Cgreen\\ [%cn]" --decorate --numstat

  # fetch and rebase current branch
  fr = "!git fetch && git rebase"

  # add and commit
  ac = "!git add -p && git commit -m "

  # full status
  s = !git status -sb && git submodule foreach --recursive git status -sb \

  # Push the current branch to the remote "origin", and set it to track the upstream branch
  publish = "!git push -u origin $(git branch-name)"

  # Delete the remote version of the current branch
  unpublish = "!git push origin :$(git branch-name)"

  # Fire up your difftool (e.g. Kaleidescope) with all the changes that
  # are on the current branch.
  code-review = difftool origin/master... \

  # Given a merge commit, find the span of commits that exist(ed) on that
  # branch. Again, not so useful in itself, but used by other aliases.
  merge-span = "!f() { echo $(git log -1 $2 --merges --pretty=format:%P | cut -d' ' -f1)$1$(git log -1 $2 --merges --pretty=format:%P | cut -d' ' -f2); }; f" \

  # Find the commits that were introduced by a merge
  merge-log = "!git log `git merge-span .. $1`"

  # Show the changes that were introduced by a merge
  merge-diff = "!git diff `git merge-span ... $1`"

  # As above, but in your difftool
  merge-difftool = "!git difftool `git merge-span ... $1`" \

  # Interactively rebase all the commits on the current branch
  rebase-branch = "!git rebase -i `git merge-base master HEAD`" \

  # Unstage any files that have been added to the staging area
  unstage = reset HEAD

  # Show changes that have been staged
  diffc = diff --cached

  # Mark a file as "assume unchanged", which means that Git will treat it
  # as though there are no changes to it even if there are. Useful for
  # temporary changes to tracked files
  assume = update-index --assume-unchanged
  # Reverse the above
  unassume = update-index --no-assume-unchanged
  # Show the files that are currently assume-unchanged
  assumed = "!git ls-files -v | grep ^h | cut -c 3-"\

  # Checkout our version of a file and add it
  ours = "!f() { git checkout --ours $@ && git add $@; }; f"
  # Checkout their version of a file and add it
  theirs = "!f() { git checkout --theirs $@ && git add $@; }; f"\

  # Cleanup local branch
  branch-cleanup = "!git fetch origin --prune && git branch --merged origin/master | grep -v 'master$' | xargs git branch -d"
```
