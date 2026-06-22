
🧠 Quick Comparison
Command	Purpose	Example Use
stash	Temporarily save uncommitted work	Switch branches without committing
squash	Combine multiple commits into one	Clean history before merging
cherry-pick	Copy specific commits to another branch	Apply hotfix across branches


Perfect—here’s a single mini practice lab you can run in terminal that covers:

🧳 git stash
🧼 git squash
🍒 git cherry-pick

We’ll use a tiny project with simple text files so you can clearly see what’s happening.

🧪 STEP 0: Setup repo
mkdir git-practice-lab
cd git-practice-lab
git init
🌿 STEP 1: Create base files (main branch)
echo "Home v1" > home.txt
echo "Login v1" > login.txt
git add .
git commit -m "Initial commit"
🌳 STEP 2: Create 3 branches (A, B, C)
git checkout -b A
git checkout -b B
git checkout -b C

Now you have:

A = feature branch (stash practice)
B = messy commits (squash practice)
C = cherry-pick source
🧳 PART 1: GIT STASH PRACTICE (Branch A)
Switch to A
git checkout A
Make changes (NOT committing)
echo "Home v2 - A update" >> home.txt
echo "Login v2 - A update" >> login.txt

Check status:

git status
💾 Stash the work
git stash

Now workspace is clean.

Switch to another branch (simulate interruption)
git checkout B

Then come back:

git checkout A
📦 Restore work
git stash pop

Now your changes are back.

🧼 PART 2: GIT SQUASH PRACTICE (Branch B)
Switch to B
git checkout B
Make multiple commits (messy history)
echo "Login fix 1" >> login.txt
git add .
git commit -m "fix login typo"

echo "Login fix 2" >> login.txt
git add .
git commit -m "adjust login UI"

echo "Login fix 3" >> login.txt
git add .
git commit -m "final login polish"

Check history:

git log --oneline
🧼 Squash commits into one
git rebase -i HEAD~3

You will see:

pick commit1 fix login typo
pick commit2 adjust login UI
pick commit3 final login polish

Change to:

pick commit1 fix login typo
squash commit2 adjust login UI
squash commit3 final login polish

Save & exit.

✅ Result:

Now you get ONE clean commit like:

Clean login feature

Check:

git log --oneline
🍒 PART 3: GIT CHERRY-PICK (Branch C → A & B)
Switch to C
git checkout C
Create two commits
echo "Hotfix: login crash fixed" >> login.txt
git add .
git commit -m "hotfix login crash"

echo "Refactor: improve logs" >> login.txt
git add .
git commit -m "improve logging"

Check commits:

git log --oneline

Example:

a1b2 hotfix login crash
c3d4 improve logging
🍒 Pick only hotfix commit into A
git checkout A
git cherry-pick <hotfix-commit-id>
🍒 Also apply to B
git checkout B
git cherry-pick <hotfix-commit-id>
🧠 WHAT YOU JUST PRACTICED
🧳 stash
Save unfinished work
Switch branches safely
Restore later
🧼 squash
Combine multiple commits into one clean commit
Used before merging PRs
🍒 cherry-pick
Copy specific commit to another branch
Used for hotfixes
🚀 OPTIONAL CHALLENGE (highly recommended)

Try this combo:

Modify A
Stash it
Apply cherry-pick from C to A
Then pop stash back