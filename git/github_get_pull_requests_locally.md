# How to fetch pull request locally

GitHub provides a special pulls remote "namespace" on the upstream repo, so you can add it as a fetch pattern to your .git/config like so:

    [remote "upstream"]
      url = https://github.com/neovim/neovim.git
      fetch = +refs/heads/*:refs/remotes/upstream/*
      fetch = +refs/pull/*/head:refs/pull/upstream/*

Then when you `git fetch --all`, you will have ALL pull requests available in your local repo in the local pull/ namespace. To check out PR #42:

    git checkout -b foo refs/pull/upstream/42

So if you don't want to use the merge button, i.e. to rewrite history locally before pushing to github, just add the requester's repo as a remote to yours.

If PR is issued from the very same repo, just add this line to the 'origin' remote:

    fetch = +refs/pull/*/head:refs/pull/origin/*
