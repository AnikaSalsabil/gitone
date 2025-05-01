# Learn Git and GitHub || Crash course from YouTube
Git:  Stores/ Points to different version of files locally- in short, Version cotnrol system

---
4 stages
1. Local / Working Directory
3. Stage (Intermediary)
4. Local Repository
5. Remote/ Cloud/ GitHub

Here, 
* Transferring changes from Working Directory to Stage  ---> Add
* Transferring changes from Stage to Local Repository ----> Commit
* Transferring changes from Local Repository to Remote ---> Push
* Transferring changes from Remote to Local Repository ---> Fetch
* Transferring ALL changes from Remote to Working Directory ---> Pull (Fetch + Merge)

---
# Work Inside Working Directory
## How to initialize git inside Local/ Working Directory:
1. Go to Git Bash
2. Type the following for creating the directory and its respective files inside local device:
``` bash
mkdir gittwo    # make directory named "gittwo"
cd gittwo       # go inside gittwo directory
touch one.txt   # create one.txt file
touch two.txt   # create two.txt file
clear
```
3. Now, to initialize git inside the directory, type the following:
``` bash
git init
```
4. In file explorer, go to the gittwo folder directory, and observe that there's a hidden folder created named ".git"
---

## How to clone git rep from github to local:
1. Go to GitHub and create a repository named "gitone" and create two text files named "one.txt" and "two.txt" with sample texts
2. Now, click on the "Code" button and copy the HTTPS git URL for cloning to local 
3. Go to Git Bash
4. Type the following for cloning the github repository inside local device:
``` bash
cd ../
git clone  https://github.com/AnikaSalsabil/gitone.git 
```
5. After that, it will successfully clone the rep to local device.
6. In file explorer, search gitone folder, and observe that the rep has been cloned
---

## How to check file changes inside local ( the rep which was cloned in prev step) 
1. Go to the file explorer and open /gitone
2. Open one.txt and change some texts and save
3. Now go to Git Bash and run the following:
```bash
cd gitone
git status
```
4. It will show the modifications that has been done inside the local rep
---
*Add:* The process of pulling changes from the Working Directory to Stage is called Add.

## How to perform Add for ALL files (local to stage)
1. Go to the Git Bash
2. Type the following commands and press enter:
```bash
cd gitone   # go to the gitone directory
ls     # check what files are inside the gitone directory
mkdir myFolder   # create another folder inside gitone
cd myFolder
touch three.txt   # create a new file three.txt inside the myFolder
pwd   # check in which directory i am inside
cd ../    # go back to one step backwards (to gitone)
git status    # check what changes have been done so far inside the gitone folder
```
3. It will show that one.txt and two.txt files are tracked (as it was cloned from github rep beforehand) but changes not staged for commit. On the other hand, myFolder/ changes are Untracked (as no changes were added to commit)
4. Now run the following in Git Bash:
```bash
git add --all     # it will take all the changes (that have been done so far) to stage OR we can use "git add -A". Does the same thing
git status       # it will show that all untracked changes have been transferred to stage (myFolder and one.txt, two.txt changes)
```
5. At this point, we are inside Stage
6. To revert back to Local, run the following:
```bash
git reset     # it will show the unstaged files after reset
git status    # it will again take us back to step-3 when some changes were tracked and some untracked files
```


## How to perform Add for specific files (local to stage)
*Dot (.)*: This operation adds all file changes that's inside the directory.
1. Go to the Git Bash
2. Type the following commands and press enter:
```bash
cd myFolder
```
3. Now run the following in Git Bash:
```bash
git add .     # it will take the specific changes made inside the myFolder directory to stage
git status       # it will show that only three.txt has been staged, but one.txt and two.txt outside myFolder are still untracked
```
5. At this point, we are inside Stage
6. To revert back to Local, run the following:
```bash
git reset     # it will show the unstaged files after reset
git status    # it will again take us back to step-3 when some changes were tracked and some untracked files
```
---
*Star (*)*: This operation adds all file changes that's inside the directory, except deletion changes.
```bash
cd myFolder
git add *     
git status       
```
---
*Specific files*: This operation adds the specified file changes that are inside the directory:
```bash
cd myFolder
git add one.txt     
git status       
```

---
# Work Inside Stage
## How to Commit Changes from Stage to Local Repository

Run the following in Git Bash:
```bash
git commit -m "I made some changes to the files"
git status   # it will show that there's nothing to commit. working tree clean
```

If we want to rollback to previous state
```bash
git reset HEAD~
git status   # it will show the tracked and untracked changes
```

## Retrieve Manually Deleted file
1. Manually delete file two.txt from the file explorer
2. Go to Git Bash and check git status
3. No add that deletion changes to stage by running the "git add ." command
4. Now, again, check git status
5. Now, as we need to retrieve the file in my file explorer, run the following command:
```bash
git reset --hard   
```
6. It will return back the file to the file explorer.

## Remove files 
1. Go to bash
2. Run the following commands in Git bash:
```bash
git rm two.txt  # removes the file
git status
```
3. In this case, we don't need to run the git add command again to add the changes to the stage (like we did in the previous section). The status will show that everything has been staged already.

*Force Remove*
1. Again, run the following:
```bash
git reset --hard  # hard reset everything
```
2. Now change something inside the two.txt file from file explorer and save
3. If I want to remove the file two.txt by running git rm two.txt, it will not allow me. Instead, it will throw an error that the respective file has some local modifications which hasn't been staged yet.
4. So, in this case- if we want to forcefully remove that file even though i am well aware that my changes hasn't been staged. we need to run the following from Git Bash:
```bash
git rm two.txt -f
```
5. Now the file has been removed.
6. Again I will hard reset to restore the two.txt file

*Cache Remove*
1. Change something inside two.txt
2. Run the following
```bash
git rm --cached two.txt
git status
```
3. Interestingly, it didnt show any error and says that the file is removed. But, in the explorer- we still can see the two.txt file. 
4. The main reason for caching here is- I want to delete the file from stage, but i dont want to remove the file from my working directory.

# Work Inside Local Repository
## Branching with Git
How many branches are there?
```bash
git branch   # asterisk denotes that the rep has only one branch which is main
```
Create a new branch named "development"
```bash
git branch development
git branch    # it will show that there are two branches now- development and *main
```
How to switch to specific branch
```bash
git checkout development   # it will switch the user to development branch (from main)
```
Git has control over files Visibility in local device
1. Assuming, I am currently inside development branch
2. In Git bash,
   ```bash
  touch three.txt   # create three.txt file inside gitone (development branch)
   ```
3. Now, add some text inside the three.txt file from file explorer
4. Check git status- that it has some untracked changes
5. Now, run the following in Git Bash to stage the changes (mandatory step for this section)
```bash
git add .
git commit -m "I created three.txt and added three there"
git status
```
6. Now, checkout to main branch from development branch by running the following bash commands:
```bash
git checkout main
```
7. Observe the file explorer of gitone directory
8. It is not showing the three.txt anymore. Because, three.txt has been created in development branch, so as we switched to main- its not displaying there.
This is the beauty of Git.

## Merging on Development branch with Main (with Merge Conflict scenario)
1. Assuming I am currently inside the main branch.
2. Now, change something inside the two.txt and check the git status
3. Checkout to the development branch again.
4. Now, check two.txt has different changes.
5. At this moment, we want to merge the changes of the development branch to the main branch
```bash
git merge main -m "merging on development with main"
```
6. Omg I got a Merge conflict!! because i made changes in the same lines of the same files.
7. Inside the two.txt file, I can see the following content:
```bash
<<<<<<< HEAD
two
2
=======
two -1 -2
>>>>>>> main
```
8. Now, we need to resolve the conflict manually. Firstly, need to decide which content to keep (or combine both) and then remove the conflict markers <<<<<<<, =======, and >>>>>>>.
9. Change the file content of two.txt and save:
```bash
two 2 combining both dev and main
```
10. Now mark the conflict as resolved by running the following from Git Bash:
```bash
git add .
git commit -m "Resolved the merge conflict"
```
11. Now try again to merge the development with main branch:
```bash
git merge main -m "Merging on development with main after resolving the conflict"
```
12. Now the merge with main branch will be successful.

## Merging on Main branch with Main 
1. Check out to main branch now and check the content of two.txt:
```bash
two -1 -2
```
2. Now merge on main branch with the development branch by running the following command in Git bash:
```bash
git merge development -m "Merging on main with development"
```
3. Now the on main branch, the changes have been merged with development.

 
# Work Inside Remote
At this moment, we want to transfer the changes from the stage (local repository) to the remote (GitHub). This process is called "Push".
1. Go to Git Bash and run the following command:
```bash
git push origin main    # it will push the changes of the main branch to the Remote (GitHub)
git checkout staging
git push origin staging   # it will create the staging branch in the remote firstly (as there's no other branch except main in the remote) and then push changes accordingly
git checkout development
git push origin development   # it will create the development branch in the remote firstly and then push changes accordingly
```
2. If there's any conflict that prevents pushing the respective changes to remote, we can resolve it in two ways:
- Option-1:
```base
git pull origin main --rebase   #Brings remote changes into your local branch without a messy merge commit.
git push origin main    #Now your branch is up-to-date, so push works.
```
- Option-2:
```base
git push origin main --force    # If you're 100% sure your local version is correct and want to overwrite the remote forcefully 
```
3. 
4. 

