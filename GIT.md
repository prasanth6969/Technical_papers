# Git Notes

- git init = This command used to initialize git into folder

---

git has four stags :

1. working directory =  the files you edit
2. stagging area = In this  we can commit our files into local area
3. local area = In this area all files has been stored locally from this we push to remote repo
4. remote area = In this area our files or projects stored in cloud server so that we can revert whenever you want

---

- git add filename = adding files into commit area
- git commit -m "mssg" = commiting to local area
- git push origin main = pushing into remote repo

---

- branch = branch is like a separate accessbility area through our branch we can make changes individually after then merge into main branch
- git checkout -b "branch name" = we can create branch
- git branch = shows all branch in our repo
- git merge branch name = combines branch into current branch
- git branch -d name = delete a merged branch

---

- git clone "url" = copy  from remote repo to local repo
- git fetch = used to check what changes has been in remote
- git pull = used to check and merge the new changes

---

- git restore file = resets a file in your working directory back to the last committed
- git restore --staged file = Undoes git add. The file leaves the staging area, but your edits stay in the file.
- git reset --soft HEAD~1 = undo the commit , keep everthing staged
- git reset --hard HEAD~1 = undo the commit and delete the changes

---

- git commit --amend -m  "better mssg
- git add forgetten.txt then
- git commit --amend --no-edit (keeps last msg)

---

- git.gitignore = this is like a text file is used to say the git to ignore node and modules
