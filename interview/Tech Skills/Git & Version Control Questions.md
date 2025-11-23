1. What's Git and why is it used?
> Git is a distributed version control system that tracks changes in source code and allows multiple developers to collaborate efficiently. It helps manage versions, rollbacks, and parallel development through branching.

2. Explain the difference between Git and Github
> Git is the underlying version control system - a command-line tool - while GitHub is a cloud-based hosting platform for Git repositories, providing collaboration features like pull requests and issue tracking.

3. What's the difference between `git merge` and `git rebase`?
> `merge` combines changes from one branch into another by creating a new commit that preserves history. `rebase` moves or reapplies commits on top of another branch, creating a linear history. Rebase gives cleaner logs, but it rewrites commit history.

4. What's the difference between `git fetch` and `git pull`?
> `fetch` downloads changes from the remote but doesn't modify your working branch. `pull` does both - it fetches and merges changes into your current branch.

5. What does `git stash` do?
> It temporarily saves your uncommited changes so you can switch branches or pull updates without losing your work. You can later restore them using `git stash apply` or `git stash pop`

6. How do you resolve a merge conflict?
> When Git can't automatically combine changes, it marks the conflict in the affected files. You manually edit those files to choose or merge changes, mark them as resolved with `git add`, and then complete the merge with `git commit`.

7. What's a detached HEAD state?
> It happens when you check out a specific commit instead of a branch. You can view or experiment with code there, but commits made in this state aren't attached to any branch unless you explicitly create one.

8. How do you undo a commit that was already pushed?
> If it's safe to rewrite history, you can use `git reset --hard <commit>` and force push. Otherwise, you should use `git revert <commit>` to create a new commit that undoes the previous one without altering history.

9. What's the difference between `git reset`, `git revert`, and `git checkout`
> - `reset` moves the branch pointer and optionally changes the staging area and working directory
> - `revert` creates a new commit that undoes previous changes
> - `checkout` switches branches or restores files from a specific commit (`git restore` is used nowadays instead)