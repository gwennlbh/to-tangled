# to-tangled
push to a tangled.sh mirror

## Inputs

| | | Default value | Example |
|--|--|--|--|
| repo | path to the repo (without the leading `@`) | (required) | tangled.sh/core
| knot | hostname of the tangled knot used | tangled.sh | 
| ssh-key | contents of a private ssh key that has push access to the repo | (required) | `-----BEGIN OPENSSH PRIVATE KEY-----\n you really thought, huh? \n-----END OPENSSH PRIVATE KEY-----`

## Quickstart

### One-click setup

If:
- you're on Linux,
- you've created a SSH key with just `ssh-keygen` without any flags,
- you have [the `gh` CLI](https://cli.github.com) installed, and
- you're on the root of your repository

```bash
gh secret set TANGLED_KEY < ~/.ssh/id_ed25519
mkdir -p .github/workflows
echo -e 'name: Tangle\n\non:\n  push: {}\n  workflow_dispatch: {}\n\njobs:\n  tangle:\n    runs-on: ubuntu-latest\n    steps:\n      - uses: gwennlbh/to-tangled@v0.3\n        with:\n          repo: yourself.bsky.social/your-repo\n          ssh-key: ${{ secrets.TANGLED_KEY }}\n' > .github/workflows/tangle.yml
# don't forget to change yourself.bsky.social/your-repo to the tangled.sh repo before committing this!!!
```

### Step by step

1. Create a secret named `TANGLED_KEY` that has your SSH private key

Quick copy if you've created a key with just `ssh-keygen` without any flags:

(linux)

```
wl-copy < ~/.ssh/id_ed25519
```

(mac os)

```
pbcopy < ~/.ssh/id_ed25519
```

(wind*ws)

```
cat ~/.ssh/id_ed25519 | clip.exe
```

Go to your github repo's settings > secrets > actions > repository secrets

2. Create the tangled.sh repo (for now, you have to do it manually beforehand)

3. Just put ~~the fries in the bag~~ this in `.github/workflows/tangle.yml`

```yaml
name: Tangle

on:
  push: {}
  workflow_dispatch: {}

jobs:
  tangle:
    runs-on: ubuntu-latest
    steps:
      - uses: gwennlbh/to-tangled@v0.3
        with:
          repo: yourself.bsky.social/your-repo
          ssh-key: ${{ secrets.TANGLED_KEY }}
```

## How?

The action clones your repo, sets up the ssh key, adds the knot as a git remote, and pushes with [`git-push --mirror`](https://man.archlinux.org/man/git-push.1#:~:text=refs/heads/foo%20doesn%E2%80%99t%20exist.-,%2D%2Dmirror,-Instead%20of%20naming)

## Thanks

to [stream.place](https://stream.place) for [their workflow file](https://github.com/streamplace/streamplace/blob/0e6712a8ecf21a9942bb0a589a75791aa5290733/.github/workflows/sync-tangled.yaml) that i did not just steal haha totes not

## License

MIT
