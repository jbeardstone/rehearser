# rehearser scripts

The following branches are available:

- main: the current branch
- initial: extracted original algo.md file
- step-01: First step of structuration + rewrite README.md
- step-02: Second step of structuration
- dev-python: python source code
- dev-ts: typescript source code

to clone the repo

```bash
git clone https://github.com/jbeardstone/rehearser.git
# OR (this methode require some more configuration)
git clone git@github.com:jbeardstone/rehearser.git
```

to get the list of all branches available:

```bash
git branch -v 
```

to switch between branches:

```bash
git checkout <branch name> 
```

to merge branch into an other:

```bash
# lets create a new branch
git checkout -b new-branch
# merge dev-ts to the new-branch
git merge dev-ts
```

to delete a local branch

```bash
git branch --delete new-branch
# or
git branch -d new-branch
```

