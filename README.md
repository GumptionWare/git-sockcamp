# Jeff's Git Sockcamp

Experiments and lessons-learned with git.

## 1. git push "un-do"

**Problem statement**: Ugh! My colleague just told me that a push I did a couple of weeks ago had junk in it that doesn't belong in our repo. I need to pull back that push without disturbing the rest of our repo.

### The Plan

To simulate this scenario, I'll create three text files and push them to the remote repository.

After the third `git push`, I'll claw back that second push.

```
% echo "# git-sockcamp" >> About.md
% echo "# kill-sockcamp" >> KillThis.md
% echo "# Sockcamp Outline" >> Outline.md
% git status
On branch main
Untracked files:
  (use "git add <file>..." to include in what will be committed)
	About.md
	KillThis.md
	Outline.md
% git add About.md
% git commit -m "About.md initial commit"
[main 00817ee] About.md initial commit
 1 file changed, 1 insertion(+)
 create mode 100644 About.md
% git push origin main 
Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Delta compression using up to 10 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 296 bytes | 296.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
To https://github.com/GumptionWare/git-sockcamp.git
   472cea6..00817ee  main -> main
% 
% git add KillThis.md
% git commit -m 'Add KillThis.md'
[main bd356db] Add KillThis.md
 1 file changed, 1 insertion(+)
 create mode 100644 KillThis.md
% git push origin main 
Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Delta compression using up to 10 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 330 bytes | 330.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
To https://github.com/GumptionWare/git-sockcamp.git
   00817ee..bd356db  main -> main
# I also set remote to origin/main   
branch 'main' set up to track 'origin/main'.
%
% git add Outline.md
% git add README.md
% git commit -m 'Ouline.md (new): README updates'
[main d14a90e] Ouline.md (new): README updates
 2 files changed, 20 insertions(+)
 create mode 100644 Outline.md
 % git push
Enumerating objects: 6, done.
Counting objects: 100% (6/6), done.
Delta compression using up to 10 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (4/4), 909 bytes | 909.00 KiB/s, done.
Total 4 (delta 0), reused 0 (delta 0), pack-reused 0
To https://github.com/GumptionWare/git-sockcamp.git
   bd356db..d14a90e  main -> main
%
% # OK, now let's "un-do" the bad push:
% # SHA of KillSockcamp.md commit: bd356db3cec27ad7dd236b507724ccbda0134228
% git revert bd356db3cec27ad7dd236b507724ccbda0134228
[main d6f86e5] Revert "Add KillThis.md"
 1 file changed, 1 deletion(-)
 delete mode 100644 KillThis.md
% 
% #After completing the prompt for the commit message:
% git status
On branch main
Your branch is ahead of 'origin/main' by 1 commit.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean
%
% git push
Enumerating objects: 3, done.
Counting objects: 100% (3/3), done.
Delta compression using up to 10 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (2/2), 275 bytes | 275.00 KiB/s, done.
Total 2 (delta 1), reused 0 (delta 0), pack-reused 0
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To https://github.com/GumptionWare/git-sockcamp.git
   8fbe711..d6f86e5  main -> main

```

**Success!!**
Looking in GitHub, I see the "KillThis.md" file is gone.

Use git to determine what the local repo thinks it has:
```
% git ls-files
About.md
Outline.md
README.md
```
Kewl, eh?

