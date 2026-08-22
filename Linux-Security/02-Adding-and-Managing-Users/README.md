# Adding and managing users with Linux commands
Scenario
In this scenario, a new employee with the username `researcher9` joins an organisation. I have to add them to the system and continue to manage their access during their time with the organisation.

Here’s how I will do this task: First, I’ll add a new employee to the system and then to their primary group. Second, I’ll make this employee the owner of a file related to a particular project. Third, I’ll add the new employee to a supplementary group. Finally, I’ll delete the employee from the system. 

# Task 1. Add a new user

<img width="618" height="60" alt="Screenshot 2026-08-21 152125" src="https://github.com/user-attachments/assets/a52e7a77-3044-4b28-962b-2dc3ff58459f" />

Firstly, I added the new user called `researcher9` to the system by running the command `sudo useradd researcher9`

Next, I used the `usermod` command with the `-g` option to add `researcher9` to the research_team group as their primary group. To do this, I ran the command `sudo usermod -g research_team researcher9`. I used `-g` because I was adding `researcher9` to the research_team as their primary group. `research_team` is the first argument, which comes directly after the `-g` option, and it indicates the group to add the new user, `researcher9`, to, which is the second argument. 

# Task 2. Assign file ownership

The new employee, `researcher9`, will take responsibility for `project_r.txt`. The `project_r.txt` file is located in the `/home/researcher2/projects` directory and is owned by the `researcher2` user. 

<img width="811" height="93" alt="Screenshot 2026-08-21 153010" src="https://github.com/user-attachments/assets/d2f67bfe-5582-44ba-881b-9440022fe371" />

To change the ownership of the `project_r.txt` file, I first used the `cd` command, followed by the absolute path, to move into the projects directory, which holds the `project_r.txt` file. I did this by running the command `cd /home/researcher2/projects`. I then ran the `ls` command to confirm the `project_r.txt` file was present. 

Next, I ran the command `sudo chown researcher9 project_r.txt` to make `researcher9` the owner of the `project_r.txt` file. Alternatively, I could have run the command `sudo chown researcher9 /home/researcher2/projects/project_r.txt`, but because I already used the `cd` command to move into the directory holding the `project_r.txt` file, I did not need to do this. 

# Task 3. Add the user to a secondary group

A couple of months later, this employee's role at the organisation has changed, and they are working in both the Research and the Sales departments. 

<img width="840" height="109" alt="Screenshot 2026-08-21 154505" src="https://github.com/user-attachments/assets/68276f5e-de84-4290-a9bc-a99215036d57" />

To add the user to the `sales_team` as a secondary group, I ran the command `sudo usermod -a -G sales_team researcher9`. By using `-a` with `-G` I ensure that the new group was added, but existing groups were not replaced. If I did not include `-a`, then any secondary group I listed in this command would replace any existing secondary groups `researcher9` was in. 

# Task 4. Delete a user

A year later, `researcher9` decided to leave the company. 

<img width="864" height="163" alt="Screenshot 2026-08-21 155108" src="https://github.com/user-attachments/assets/36db741a-beda-4ba6-853b-bc094c788c68" />

I first ran the command `sudo userdel researcher9` to delete the user from the system. This prompted the message: `group researcher9 not removed because it is not the primary group of user researcher9`. I then ran `sudo groupdel researcher9` to remove the empty group.

When creating a new user, a group with the same name as the user is automatically created, and the user is the only member of that group. After removing the user, I cleaned up by removing the empty group that was left behind. 

# Summary 

In this activity, I learned how to manage users, groups, and files in Linux. First, I created a new user using `sudo useradd researcher9`. Next, I used `cd` to move into the folder and changed the file owner using `sudo chown researcher9 project_r.txt`. Then, I added the user to a new group using `sudo usermod -a -G sales_team researcher9`, keeping the `-a` flag so I didn't erase their old groups. Finally, I deleted the user with `sudo userdel researcher9` and removed their leftover empty group using `sudo groupdel researcher9`. 











 
