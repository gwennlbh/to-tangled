# to-tangled
push to a tangled.sh mirror

## Inputs

| | | Default value | Example |
|--|--|--|--|
| repo | path to the repo (without the leading `@`) | (required) | tangled.sh/core
| knot | hostname of the tangled knot used | tangled.sh | 
| ssh-key | contents of a private ssh key that has push access to the repo | (required) | `-----BEGIN OPENSSH PRIVATE KEY-----\n you really thought, huh? \n-----END OPENSSH PRIVATE KEY-----`

## How?

The action clones your repo, sets up the ssh key, adds the knot as a git remote, and pushes with [`git-push --mirror`](https://man.archlinux.org/man/git-push.1#:~:text=refs/heads/foo%20doesn%E2%80%99t%20exist.-,%2D%2Dmirror,-Instead%20of%20naming)

