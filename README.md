# git-flow-release

GitHub CLI extension to collaborate with git-flow release safely.

## Install

```console
gh extension install u-minor/gh-gfr
```

## Prerequisites

- git-flow-avh
- node and npx

## Usage

```console
Usage: gh gfr [-r <reviewers>] <version>
    reviewers: List of GitHub user ID (<uid>[,<uid>...])
    version: <newversion>|major|minor|patch|premajor|preminor|prepatch|prerelease
```

```console
gh gfr -r foo,bar,baz minor
```

When your project has package.json or build.sbt, you can use semver string for new version.

### Internal process

1. Generate new version from semver string
   - Only when package.json or build.sbt exists
2. Start git-flow release
3. Update package version
   - Only when package.json or build.sbt exists
4. Finish git-flow release
   - Keep release branch to create PR
5. Push release branch to GitHub
6. Create PR (release -> master) and wait approve (#PR1)
   - Do not merge #PR1 on GitHub!
7. Push master branch to GitHub
   - #PR1 is closed automatically
8. Create PR (master -> develop) and wait approve (#PR2)
   - Do not merge #PR2 on GitHub!
9. Push develop branch to GitHub
   - #PR2 is closed automatically
10. Cleanup release branch
