# gitalias
Some alias very useful

## alias

### git fr
This alias allow to fetch and rebase with logs

```sh
fr = "!f() { \
    trap 'echo ERROR: Operation failed; return' ERR; \
    \
    echo ---- Fetching on branch $(git branch-name) ----;\
    git fetch;\
    echo ---- Rebasing branch $(git branch-name) ----;\
    git rebase;\
    };
```

### git switch
Allow to change branch with a fetch and rebase

```sh
switch = "!f() { \
    trap 'echo ERROR: Operation failed; return' ERR; \
    \
    [ -z \"$1\" ] && echo \"branch name required, e.g develop, master, feature/XXX, ...\" && exit 1; \
    echo ---- Switching to branch $1 ----; \
    git checkout $1;\
    git fr;\
    };
```

### git s
Display a inline status of your git status

```sh
s = !git status -sb && git submodule foreach --recursive git status -sb
```