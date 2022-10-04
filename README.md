# Jeff's Git Sockcamp

Experiments and lessons-learned with git.

## First off: git push "un-do"

Problem statement: Ugh! My colleague just told me that a push I did a couple of weeks ago had junk in it that doesn't belong in our repo. I need to pull back that push without disturbing the rest of our repo.

### The Plan

To simulate this scenario, I'll create three text files and push them to the remote repository.

After the third `git push`, I'll claw back that second push.

<code>
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

