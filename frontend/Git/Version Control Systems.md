Git stores changes as snapshots as opposed to diffs like in other VCS.

## Strategies

## Commands

### Init

The **`--bare`** flag creates a repository that doesn’t have a working directory, making it impossible to edit files and commit changes in that repository. You would create a bare repository to git push and git pull from, but never directly commit to it. Central repositories should always be created as bare repositories because pushing branches to a non-bare repository has the potential to overwrite changes. Think of `--bare` as a way to mark a repository as a storage facility, as opposed to a development environment. This means that for virtually all Git workflows, the central repository is bare, and developers local repositories are non-bare.

**Templates** allow you to initialize a new repository with a predefined `.git` subdirectory. You can configure a template to have default directories and files that will get copied to a new repository's `.git` subdirectory. The default Git templates usually reside in a `` `/usr/share/git-core/templates` `` directory but may be a different path on your machine.

### Clone

`git clone <repo> <directory>`
`git clone --branch <tag> <repo>`

`git clone -depth=1 <repo>` - Clone the repository located at `＜repo＞` and only clone the  history of commits specified by the option depth=1. In this example a clone of `＜repo＞` is made and only the most recent commit is included in the new cloned Repo. Shallow cloning is most useful when working with repos that have an extensive commit history. An extensive commit history may cause scaling problems such as disk space usage limits and long wait times when cloning. A Shallow clone can help alleviate these scaling issues.

Passing the `--mirror` argument implicitly passes the `--bare` argument as well. This means the behavior of `--bare` is inherited by `--mirror`. Resulting in a bare repo with no editable working files. In addition, `--mirror` will clone all the extended refs of the remote repository, and maintain remote branch tracking configuration. You can then run `git remote` update on the mirror and it will overwrite all refs from the origin repo. Giving you exact 'mirrored' functionality.

