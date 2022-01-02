Initialization
===

    # Create Local Branches from Remotes
    git branch -r --list $1 | grep -vE "HEAD|master" \
        | perl -pe "s/^\s*(\w+?\/(.*))/git branch \2 \1/g;" \
        | $SHELL;

    # Create Worktree
    git branch --list $1 | grep -v master | cut -c3- \
        | perl -pe "s/^\s*(.*)/git worktree add \1 \1/g;" \
        | $SHELL;

Updates
===

    git branch | perl -pe "s#^..##g;" \
        | xargs -rt -I{} git push -v gh {};
