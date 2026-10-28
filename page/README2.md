1. Aim
To perform version control operations using Git.
2. Procedure
Step 1: Check the Git version

git --version


Information: Checks whether Git is installed on the system and displays its version.

If Git is not installed on Ubuntu, follow Step 2.
Step 2: Install Git on Ubuntu (if required)

sudo apt update
sudo apt install git -y


Information: Updates the package list and installs Git on Ubuntu.

After installation, check again:

git --version


Step 3: Create a directory

mkdir example
cd example


Information: Creates a directory named example and enters it.
Step 4: Create a file

vim calc.sh


Write the following content:

x=a+b


Press Esc, type :wq, and press Enter to save the file.

Information: Creates a file named calc.sh.
Step 5: Initialize the Git repository

git init


Information: Initializes a Git repository in the current directory.
Step 6: Check the file status

git status


Information: Displays the current status of files in the repository.
Step 7: Add the file

git add calc.sh


Information: Adds the file to the staging area.
Step 8: Configure the Git user

git config --global user.name "Your Name"
git config --global user.email "you@example.com"


Information: Configures the username and email used for commits. Replace the example values with your own details.
Step 9: Commit the first version

git commit -m "first version"


Information: Records the first version of the file in Git history.
Step 10: Modify the file

vim calc.sh


Change the content to:
x=a+b+c


Save the file using Esc, :wq, and Enter.

Step 11: Commit the second version

git add calc.sh
git commit -m "second version"


Information: Records the modified version in Git history.
Step 12: View commit history

git log


Information: Displays previous commits, commit IDs, and messages.
Step 13: Restore an earlier version
Find the required commit ID using git log, then run:

git restore --source=COMMIT_ID -- calc.sh


Replace COMMIT_ID with the actual commit ID.

Information: Restores the file content from the selected commit.
Step 14: Check the final status

git status
