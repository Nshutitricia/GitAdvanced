# Git Advanced Exercises

## Part 1

### Missing File Fix

```bash
user@DESKTOP-8NS2V24 MINGW64 ~/Documents/Git Exercises/GitAdvancedSample (main)
$ git status
On branch main
Your branch is based on 'origin/main', but the upstream is gone.
  (use "git branch --unset-upstream" to fixup)

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        README.md
        test4.md

nothing added to commit but untracked files present (use "git add" to track)

user@DESKTOP-8NS2V24 MINGW64 ~/Documents/Git Exercises/GitAdvancedSample (main)
$ git log
commit 0c1979facfa2c46ecb315959133a83040e401062 (HEAD -> main)
Author: Nshutitricia <nshutricia@gmail.com>
Date:   Wed Mar 5 10:48:58 2025 +0200

    chore: Create third and fourth files

commit 78b2ddc71211dbcc138b528ba4d7168aca7c9791
Author: Nshutitricia <nshutricia@gmail.com>
Date:   Wed Mar 5 10:48:57 2025 +0200

    chore: Create another file

commit 5f29d5ada92a0bd76f3ca58dc9dca5bc60562740
Author: Nshutitricia <nshutricia@gmail.com>
Date:   Wed Mar 5 10:48:57 2025 +0200

    chore: Create initial file

user@DESKTOP-8NS2V24 MINGW64 ~/Documents/Git Exercises/GitAdvancedSample (main)
$ git add test4.md && git commit -m "chore: Create fourth file"
[main b3f3365] chore: Create fourth file
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 test4.md
```

### Editing Commit History

```bash
reword 78b2ddc chore: Create another file
chore: Create second file

user@DESKTOP-8NS2V24 MINGW64 ~/Documents/Git Exercises/GitAdvancedSample (main)
$ git rebase -i HEAD~3
[detached HEAD 6ceeb7f] chore: Create second file
 Date: Wed Mar 5 10:48:57 2025 +0200
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 test2.md
Successfully rebased and updated refs/heads/main.

user@DESKTOP-8NS2V24 MINGW64 ~/Documents/Git Exercises/GitAdvancedSample (main)
$ git log
commit 29495a07e96cd91ddac670e4b0e971b068371718 (HEAD -> main)
Author: Nshutitricia <nshutricia@gmail.com>
Date:   Wed Mar 5 10:53:16 2025 +0200

    chore: Create fourth file

commit 83ca929ec0b38c80224d95871a15cb23cf6baa56
Author: Nshutitricia <nshutricia@gmail.com>
Date:   Wed Mar 5 10:48:58 2025 +0200

    chore: Create third and fourth files

commit 6ceeb7f635c2d663c055889093473be986f333e9
Author: Nshutitricia <nshutricia@gmail.com>
Date:   Wed Mar 5 10:48:57 2025 +0200

    chore: Create second file

commit 5f29d5ada92a0bd76f3ca58dc9dca5bc60562740
Author: Nshutitricia <nshutricia@gmail.com>
Date:   Wed Mar 5 10:48:57 2025 +0200

    chore: Create initial file
```

### Keeping History Tidy - Squashing Commits

```bash
Used github desktop
PS C:\Users\user\Documents\Git Exercises\GitAdvancedSample> git log --oneline
f59e774 (HEAD -> main) chore: Create fourth file
d94f8d2 chore: Create third and fourth files
07062c5 chore: Squashed files
```

### Splitting a Commit

```bash
PS C:\Users\user\Documents\Git Exercises\GitAdvancedSample> git reset --soft HEAD^
PS C:\Users\user\Documents\Git Exercises\GitAdvancedSample> git status
On branch main
Your branch and 'origin/main' have diverged,
and have 2 and 4 different commits each, respectively.
  (use "git pull" if you want to integrate the remote branch with yours)

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   test4.md

PS C:\Users\user\Documents\Git Exercises\GitAdvancedSample> git reset --soft HEAD^
PS C:\Users\user\Documents\Git Exercises\GitAdvancedSample> git status
On branch main
Your branch and 'origin/main' have diverged,
and have 1 and 4 different commits each, respectively.
  (use "git pull" if you want to integrate the remote branch with yours)

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   test3.md
        new file:   test4.md

PS C:\Users\user\Documents\Git Exercises\GitAdvancedSample> git log --oneline
07062c5 (HEAD -> main) chore: Squashed files
PS C:\Users\user\Documents\Git Exercises\GitAdvancedSample> git restore --staged test3.md 
PS C:\Users\user\Documents\Git Exercises\GitAdvancedSample> git restore --staged test4.md
PS C:\Users\user\Documents\Git Exercises\GitAdvancedSample> git status 
On branch main
Your branch and 'origin/main' have diverged,
and have 1 and 4 different commits each, respectively.
  (use "git pull" if you want to integrate the remote branch with yours)

Untracked files:
  (use "git add <file>..." to include in what will be committed)       
        test3.md
        test4.md

nothing added to commit but untracked files present (use "git add" to track)

$ git add test3.md && git commit -m "chore: Create Thir
d file"
[main 2b726cc] chore: Create Third file
 1 file changed, 0 insertions(+), 0 deletions(-)       
 create mode 100644 test3.md

user@DESKTOP-8NS2V24 MINGW64 ~/Documents/Git Exercises/GitAdvancedSample (main)
$ git add test4.md && git commit -m "chore: Create Four
th file"
[main 4c2d63c] chore: Create Fourth file
 1 file changed, 0 insertions(+), 0 deletions(-)       
 create mode 100644 test4.md

user@DESKTOP-8NS2V24 MINGW64 ~/Documents/Git Exercises/GitAdvancedSample (main)
$ git status
On branch main
Your branch and 'origin/main' have diverged,
and have 3 and 4 different commits each, respectively. 
  (use "git pull" if you want to integrate the remote branch with yours)

nothing to commit, working tree clean

user@DESKTOP-8NS2V24 MINGW64 ~/Documents/Git Exercises/GitAdvancedSample (main)
$ git log --oneline
4c2d63c (HEAD -> main) chore: Create Fourth file
2b726cc chore: Create Third file
07062c5 chore: Squashed files

```

### Advanced Squashing

```bash
PS C:\Users\user\Documents\Git Exercises\GitAdvancedSample> git rebase -i HEAD~2
[detached HEAD 38cb719] chore: Create third and fourth file
 Date: Wed Mar 5 12:26:20 2025 +0200
 2 files changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 test3.md
 create mode 100644 test4.md
Successfully rebased and updated refs/heads/main.      
PS C:\Users\user\Documents\Git Exercises\GitAdvancedSample> git log --oneline
38cb719 (HEAD -> main) chore: Create third and fourth file
07062c5 chore: Squashed files
```

### Dropping a Commit

```bash
user@DESKTOP-8NS2V24 MINGW64 ~/Documents/Git Exercises/GitAdvancedSample (main)
$ touch unwanted.txt

user@DESKTOP-8NS2V24 MINGW64 ~/Documents/Git Exercises/GitAdvancedSample (main)
$ git add unwanted.txt && git commit -m "unwantes Commit"
[main 703bb9d] unwantes Commit
 1 file changed, 1 insertion(+)
 create mode 100644 unwanted.txt

 user@DESKTOP-8NS2V24 MINGW64 ~/Documents/Git Exercises/GitAdvancedSample (main)
$ git rebase -i HEAD~2
Successfully rebased and updated refs/heads/main.      

user@DESKTOP-8NS2V24 MINGW64 ~/Documents/Git Exercises/GitAdvancedSample (main)
$ git log --oneline
38cb719 (HEAD -> main) chore: Create third and fourth file
07062c5 chore: Squashed files

```

### Reordering Commits

```bash
user@DESKTOP-8NS2V24 MINGW64 ~/Documents/Git Exercises/GitAdvancedSample (main)
$ git log --oneline
0b8d74e (HEAD -> main) chore: order this
38cb719 chore: Create third and fourth file
07062c5 chore: Squashed files

user@DESKTOP-8NS2V24 MINGW64 ~/Documents/Git Exercises/GitAdvancedSample (main)
$ git rebase -i HEAD~2
Successfully rebased and updated refs/heads/main.      

user@DESKTOP-8NS2V24 MINGW64 ~/Documents/Git Exercises/GitAdvancedSample (main)
$ git log --oneline
328e3df (HEAD -> main) chore: Create third and fourth file
457518c chore: order this
07062c5 chore: Squashed files

```

### Cherry-Picking Commits

```bash

user@DESKTOP-8NS2V24 MINGW64 ~/Documents/Git Exercises/GitAdvancedSample (main)
$ git checkout -b ft/branch
Switched to a new branch 'ft/branch'

user@DESKTOP-8NS2V24 MINGW64 ~/Documents/Git Exercises/GitAdvancedSample (ft/branch)
$ touch test5.md

user@DESKTOP-8NS2V24 MINGW64 ~/Documents/Git Exercises/GitAdvancedSample (ft/branch)
$ git add test5.md && git commit -m "chore: Implement test 5"
[ft/branch a56fee8] chore: Implement test 5
 1 file changed, 1 insertion(+)
 create mode 100644 test5.md

user@DESKTOP-8NS2V24 MINGW64 ~/Documents/Git Exercises/GitAdvancedSample (ft/branch)
$ git checkout main
Switched to branch 'main'
Your branch and 'origin/main' have diverged,
and have 3 and 4 different commits each, respectively. 
  (use "git pull" if you want to integrate the remote branch with yours)

user@DESKTOP-8NS2V24 MINGW64 ~/Documents/Git Exercises/GitAdvancedSample (main)
$ git log --oneline
328e3df (HEAD -> main) chore: Create third and fourth file
457518c chore: order this
07062c5 chore: Squashed files

user@DESKTOP-8NS2V24 MINGW64 ~/Documents/Git Exercises/GitAdvancedSample (main)
$ git checkout ft/branch
Switched to branch 'ft/branch'

user@DESKTOP-8NS2V24 MINGW64 ~/Documents/Git Exercises/GitAdvancedSample (ft/branch)
$ git log --oneline
a56fee8 (HEAD -> ft/branch) chore: Implement test 5
328e3df (main) chore: Create third and fourth file     
457518c chore: order this
07062c5 chore: Squashed files

user@DESKTOP-8NS2V24 MINGW64 ~/Documents/Git Exercises/GitAdvancedSample (ft/branch)
$

user@DESKTOP-8NS2V24 MINGW64 ~/Documents/Git Exercises/GitAdvancedSample (ft/branch)
$ git checkout main
Switched to branch 'main'
Your branch and 'origin/main' have diverged,
and have 3 and 4 different commits each, respectively. 
  (use "git pull" if you want to integrate the remote branch with yours)

user@DESKTOP-8NS2V24 MINGW64 ~/Documents/Git Exercises/GitAdvancedSample (main)
$ git cherry-pick a56fee8
[main 23e827b] chore: Implement test 5
 Date: Wed Mar 5 13:06:02 2025 +0200
 1 file changed, 1 insertion(+)
 create mode 100644 test5.md

user@DESKTOP-8NS2V24 MINGW64 ~/Documents/Git Exercises/GitAdvancedSample (main)
$ git log --oneline
23e827b (HEAD -> main) chore: Implement test 5
328e3df chore: Create third and fourth file
457518c chore: order this
07062c5 chore: Squashed files
```

### Visualizing Commit History (Bonus)

```bash
$ git log --graph
* commit 23e827b0bb916946c62a5c21f555cbcb8d29ac72 (HEAD -> main)
| Author: Tricia Nshuti <nshutricia@gmail.com>
| Date:   Wed Mar 5 13:06:02 2025 +0200
| 
|     chore: Implement test 5
| 
* commit 328e3dfef6e286c434695bd9c2b8d704d03ae74c
| Author: Tricia Nshuti <nshutricia@gmail.com>
| Date:   Wed Mar 5 12:26:20 2025 +0200
|
|     chore: Create third and fourth file
|
|     chore: Create Third file
|
|     chore: Create Fourth file
|
* commit 457518cae5399c9f0c3ce1259ec96f7aa6d5ea1f      
|
* commit 328e3dfef6e286c434695bd9c2b8d704d03ae74c      
| Author: Tricia Nshuti <nshutricia@gmail.com>
| Date:   Wed Mar 5 12:26:20 2025 +0200
|
|     chore: Create third and fourth file
|
|     chore: Create Third file
|
|     chore: Create Fourth file
|
* commit 457518cae5399c9f0c3ce1259ec96f7aa6d5ea1f 

user@DESKTOP-8NS2V24 MINGW64 ~/Documents/Git Exercises/GitAdvancedSample (main)
$ git log --graph --oneline --all
* 23e827b (HEAD -> main) chore: Implement test 5
| * a56fee8 (ft/branch) chore: Implement test 5        
|/
* 328e3df chore: Create third and fourth file
* 457518c chore: order this
* 07062c5 chore: Squashed files
* 29495a0 (origin/main, origin/HEAD) chore: Create fourth file
* 83ca929 chore: Create third and fourth files
* 6ceeb7f chore: Create second file
* 5f29d5a chore: Create initial file
```

### Understanding Reflogs (Bonus)

```bash
user@DESKTOP-8NS2V24 MINGW64 ~/Documents/Git Exercises/GitAdvancedSample (main)
$ git reflog
23e827b (HEAD -> main) HEAD@{0}: checkout: moving from ft/branch to main
a56fee8 (ft/branch) HEAD@{1}: checkout: moving from main to ft/branch
23e827b (HEAD -> main) HEAD@{2}: cherry-pick: chore: Implement test 5
328e3df HEAD@{3}: checkout: moving from ft/branch to main
a56fee8 (ft/branch) HEAD@{4}: checkout: moving from main to ft/branch
328e3df HEAD@{5}: checkout: moving from ft/branch to main
a56fee8 (ft/branch) HEAD@{6}: commit: chore: Implement test 5
328e3df HEAD@{7}: checkout: moving from main to ft/branch
328e3df HEAD@{8}: rebase (finish): returning to refs/heads/main
328e3df HEAD@{9}: rebase (pick): chore: Create third and fourth file
457518c HEAD@{10}: rebase (pick): chore: order this    
07062c5 HEAD@{11}: rebase (start): checkout HEAD~2     
0b8d74e HEAD@{12}: commit: chore: order this
38cb719 HEAD@{13}: rebase (finish): returning to refs/heads/main
38cb719 HEAD@{14}: rebase (start): checkout HEAD~1     
38cb719 HEAD@{15}: rebase (finish): returning to refs/heads/main
38cb719 HEAD@{16}: rebase (start): checkout HEAD~2     
703bb9d HEAD@{17}: commit: unwantes Commit
38cb719 HEAD@{18}: rebase (finish): returning to refs/heads/main
38cb719 HEAD@{19}: rebase (squash): chore: Create third and fourth file
2b726cc HEAD@{20}: rebase (start): checkout HEAD~2     
4c2d63c HEAD@{21}: commit: chore: Create Fourth file   
2b726cc HEAD@{22}: commit: chore: Create Third file    
07062c5 HEAD@{23}: reset: moving to HEAD^
d94f8d2 HEAD@{24}: reset: moving to HEAD^
f59e774 HEAD@{25}: rebase (finish): returning to refs/heads/main
f59e774 HEAD@{26}: rebase (pick): chore: Create fourth file
d94f8d2 HEAD@{27}: rebase (pick): chore: Create third and fourth files
07062c5 HEAD@{28}: rebase (squash): chore: Squashed files
5f29d5a HEAD@{29}: rebase: fast-forward
7edeb85 HEAD@{30}: rebase (start): checkout 7edeb85573731291dfe748fe74b47699eda6e328
29495a0 (origin/main, origin/HEAD) HEAD@{31}: checkout: moving from 60f82a6604361ae7b00c1dbb863a25db6fb8aaf3 to main
60f82a6 HEAD@{32}: rebase (pick): chore: Create fourth file
65033cb HEAD@{33}: rebase (pick): chore: Create third and fourth files
ef653c3 HEAD@{34}: rebase (reword): chore: Create second file
7270579 HEAD@{35}: rebase: fast-forward
5f29d5a HEAD@{36}: rebase (start): checkout HEAD~3     
013b986 HEAD@{37}: rebase (pick): chore: Create fourth file
e4d1378 HEAD@{38}: rebase (pick): chore: Create third and fourth files
7270579 HEAD@{39}: rebase (reword): chore: Create another file
78b2ddc HEAD@{40}: rebase: fast-forward
5f29d5a HEAD@{41}: rebase (start): checkout HEAD~3     
b3f3365 HEAD@{42}: reset: moving to b3f3365
5f29d5a HEAD@{43}: rebase (start): checkout HEAD~3     
29495a0 (origin/main, origin/HEAD) HEAD@{44}: rebase (finish): returning to refs/heads/main
29495a0 (origin/main, origin/HEAD) HEAD@{45}: rebase (start): checkout HEAD~3
29495a0 (origin/main, origin/HEAD) HEAD@{46}: rebase (finish): returning to refs/heads/main
29495a0 (origin/main, origin/HEAD) HEAD@{47}: rebase (start): checkout HEAD~2
29495a0 (origin/main, origin/HEAD) HEAD@{48}: rebase (finish): returning to refs/heads/main
29495a0 (origin/main, origin/HEAD) HEAD@{49}: rebase (start): checkout HEAD~3
29495a0 (origin/main, origin/HEAD) HEAD@{50}: rebase (finish): returning to refs/heads/main
29495a0 (origin/main, origin/HEAD) HEAD@{51}: rebase (pick): chore: Create fourth file
83ca929 HEAD@{52}: rebase (pick): chore: Create third and fourth files
6ceeb7f HEAD@{53}: rebase (reword): chore: Create second file
78b2ddc HEAD@{54}: rebase: fast-forward
5f29d5a HEAD@{55}: rebase (start): checkout HEAD~3     
b3f3365 HEAD@{56}: rebase (finish): returning to refs/heads/main
b3f3365 HEAD@{57}: rebase (start): checkout HEAD~2     
b3f3365 HEAD@{58}: commit: chore: Create fourth file   
0c1979f HEAD@{59}: commit: chore: Create third and fourth files
78b2ddc HEAD@{60}: commit: chore: Create another file  
5f29d5a HEAD@{61}: commit (initial): chore: Create initial file

```