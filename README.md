This repo's purpose is to reproduce a rebase regression in Git 2.18.

```bash
$ git checkout branch
$ git rebase master
$ git status
```

Only file3 should be moved, not the rest of the files in `files` folder.

Here's the expected (correct) `git status` output (git version 2.15.1):

```
rebase in progress; onto baf8d2a
You are currently rebasing branch 'branch' on 'baf8d2a'.
  (fix conflicts and then run "git rebase --continue")
  (use "git rebase --skip" to skip this patch)
  (use "git rebase --abort" to check out the original branch)

Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	renamed:    files/file3 -> nested/files/file3

Unmerged paths:
  (use "git reset HEAD <file>..." to unstage)
  (use "git add <file>..." to mark resolution)

	both modified:   project

```

Here's the buggy one (git version 2.18.0):

```
rebase in progress; onto baf8d2a
You are currently rebasing branch 'branch' on 'baf8d2a'.
  (fix conflicts and then run "git rebase --continue")
  (use "git rebase --skip" to skip this patch)
  (use "git rebase --abort" to check out the original branch)

Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	renamed:    files/file1 -> nested/files/file1
	renamed:    files/file2 -> nested/files/file2
	renamed:    files/file3 -> nested/files/file3
	renamed:    files/file4 -> nested/files/file4
	renamed:    files/file5 -> nested/files/file5

Unmerged paths:
  (use "git reset HEAD <file>..." to unstage)
  (use "git add <file>..." to mark resolution)

	both modified:   project

```
