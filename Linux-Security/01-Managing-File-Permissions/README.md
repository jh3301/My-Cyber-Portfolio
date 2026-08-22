# Managing file permissions in Linux
# Project description

My task is to examine existing permissions on the file system. I will need to determine if the permissions match the authorisation that should be given. If they do not match, I’ll need to modify the permissions to authorise the appropriate users and remove any unauthorised access. 

# Check file and directory details

<img width="805" height="265" alt="Screenshot 2026-08-20 122403" src="https://github.com/user-attachments/assets/5110e792-c284-42cb-a923-ccf06992ab78" />

I used the command `ls -la` to display the current permissions for all files and subdirectories, including hidden ones, in the projects directory.



# Describe the permissions string

<img width="805" height="265" alt="Screenshot 2026-08-20 122403" src="https://github.com/user-attachments/assets/cddcc258-8a5e-4a85-88ae-0fc67d176051" />

The permissions for the file `project_k.txt` are: `-rw-rw-rw-`

The `-` at the beginning of the file indicates that this permission string is for a file; a `d` would be used to represent a directory. The 2nd-4th characters indicate the permissions for the user. In this case, the user has read and write permissions (`rw`) but does not have execute permissions (indicated by the`-`). The 5th-7th characters indicate the permissions for the group (`research_team`); in this case, it is the same as the permissions for the owner. Finally, the 8th-10th characters represent the permissions for others; in this case, they have the same permissions as the user and group. 



# Change file permissions 

<img width="791" height="281" alt="Screenshot 2026-08-20 140138" src="https://github.com/user-attachments/assets/0a1bf1a0-7553-485c-98a7-8788b6f86d62" />

For this activity, the organisation does not allow others to have write permissions to any files.

By looking through the permissions list, the `project_ k.txt` file had write permissions granted to others. To rectify this, I used the command `chmod o-w project_k.txt` to remove the write permissions for others for this file.  The `chmod` command allows me to change the permissions on files and directories. To execute this command, I used the first argument, `o-w`, to remove write (`w`) permissions from others (`o`). Removing the permissions was indicted bythe use of the minus (`-`). The second argument in this command was `project_k.txt` to indicate which file I was changing the permissions for. 

Typing the command `ls -la` again showed that write permissions for others had been removed from this file.



# Change file permissions on a hidden file

<img width="791" height="281" alt="Screenshot 2026-08-20 140138" src="https://github.com/user-attachments/assets/e0c12095-7e71-4f13-a3ae-7394cd2b76c9" />

For this activity, the research team has archived `.project_x.txt`, which is why it’s a hidden file, indicated by the period (`.`) at the beginning of the file name. This file should not have write permissions for anyone, but the user and group should be able to read the file. 

Looking at the file permissions for the hidden file, it is clear to see that the user has read and write access (`rw-`), and the group have only write access(`-w-`); others have not been granted any permissions for this file, indicated by the `---`.

Firstly, I will remove the write access to this file for the user and group. I will run the command `chmod u-w,g-w .project_x.txt` to do this.

<img width="794" height="273" alt="Screenshot 2026-08-20 142817" src="https://github.com/user-attachments/assets/bfcfb557-d07d-4edd-abdd-ceaf309f7c07" />

Running the command `ls -la` shows that write permissions have now been removed for both the user and group.

Next, I will grant read access to the group for this file. To do so, I will run the command `chmod g+r .project_x.txt`. Running `g+r` will grant the group read permissions.

<img width="789" height="271" alt="Screenshot 2026-08-20 143339" src="https://github.com/user-attachments/assets/fa5bbc31-6e60-41e1-b76d-da070c3639c9" />

Running `ls -la` one more time now confirms that the user and group have only read permissions for this file.



# Change directory permissions

For this activity, the files and directories in the projects directory belong to the researcher2 user. Only researcher2 should be allowed to access the drafts directory and its contents. 

By running `ls -la`, we can see that the drafts directory has full read, write and execute permissions for the user, but also grants execute permissions for the group. See below.

<img width="791" height="259" alt="Screenshot 2026-08-20 140138new" src="https://github.com/user-attachments/assets/711c230e-6e7a-4b0d-8a85-2a93293d9d07" />

Running the command `chmod g-x drafts` will remove the execute permissions for the group. Running `ls -la` one more time will confirm this.

<img width="795" height="273" alt="Screenshot 2026-08-20 145742" src="https://github.com/user-attachments/assets/aad11c36-b610-44af-a799-41c4fece2225" />


# Summary
In this task, I used `ls -la` to check the current permissions for all files and directories, including hidden ones. I then used the `chmod` command to fix security issues by removing write permissions from others on `project_k.txt`. Next, I updated the hidden file `.project_x.txt` so only the owner and group have read-only access. Finally, I removed group access from the drafts directory so only `researcher2` can open it. I verified all my changes with `ls -la` along the way. 

To view as a pdf click here
[File permissions in Linux.pdf](https://github.com/user-attachments/files/31269027/File.permissions.in.Linux.pdf)

