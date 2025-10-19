# TryHackMe

#### Room: [Disgruntled](https://tryhackme.com/room/disgruntled)
#### Room Level: Easy
#### Completed: 10/17/2025
#### OS Used: Ubuntu 20.04.6 LTS

## Environment/Setup
* This lab is performed using the TryHackMe-provided virtual machine (VM) directly in the browser
* No additional installation or local configuration is required

## Scope
* Access is limited to the single TryHackMe provided VM
* All actions are performed locally and limited to the filesystem
    
## Background
In this room we play the role of an investigator who is tasked with discovering any signs of malicious activity on the machine of a clients employee. This person was part of the IT department and has recently been arrested for cyber crimes. Our goal is to determine if this person has conducted any nefarious activities on their computer.

## Walkthrough 

### Question 1: 
The user installed a package on the machine using elevated privileges. According to the logs, what is the full COMMAND?
 #### Process
1. Checked the users bash history (home directory of ```cybert```) for any install commands ran
   
    ```
    cd /home/cybert
    cat .bash_history
    ```
    The output shows that the user had typed ```sudo apt install dokuwiki``` at some point. TryHackMe's expected answer requires a full command path, therefore further research was necessary. However, it was now known that the user had installed the package ```dokuwiki``` with ```sudo```. These would be the keywords used to search for the target.
2. Checked authentication logs for the keywords

    ```
    cd /var/log
    grep sudo auth.log.1 | grep dokuwiki
    ```
    Authentication logs in Linux (Debian) are stored in ```/var/log/auth.log```. Upon navigating here, ```grep``` was used to search for any potential matches using the keywords from step 1. The file, ```auth.log``` yielded no results however, there was another file to search: ```auth.log.1```. The resulting output included this entry: ```COMMAND=/usr/bin/apt install dokuwiki```. This was a full command path which satisfied the requirements of what was being searched for. Upon submitting, the answer was marked correct. Note that ```COMMAND=``` was omitted as the question just asked for the path itself.

#### Answer
* `/usr/bin/apt install dokuwiki` 


### Question 2: 
What was the present working directory (PWD) when the previous command was run?
#### Process
   1. The present working directory can be found through following the same steps from step 2 from the question before as the output of `grep sudo auth.log.1 | grep dokuwiki` also contains the directory where the command was executed. Therefore, answering the previous question answers this question as well.  The log entry shows the working directory as: `PWD=/home/cybert`.

#### Answer
* `/home/cybert`


### Question 3:
Which user was created after the package from the previous task was installed?
#### Process
1. Checked the users bash history (home directory of `cybert`) for any `adduser` commands ran
   
    ```   
    cd /home/cybert
    cat .bash_history
    ```
    Viewing the bash history, it can be seen that the `adduser` command was ran only once and this did occur after the package from the previous task was installed. This single user that was created was `it-admin`

#### Answer
* `it-admin`


### Question 4:
A user was then later given sudo privileges. When was the sudoers file updated? (Format: Month Day HH:MM:SS)
#### Process
1. Verified sudo privileges by checking the sudoers file
   
    ```
    cat /etc/sudoers
    ```
    The `/etc/sudoers` file is where users with sudo privileges are defined. I know the user who was given these privileges is not `cybert` as they had used sudo earlier. Therefore, I am looking for another user. Upon viewing the file, the only users listed are `root`, `cybert` and `it-admin`. In this case, `it-admin` should be the user who was given the privileges.

2. Confirm who updated the sudo file
   
   ```
   cd /home/cybert
   cat .bash_history
   ```
   Since user `it-admin` was added to the sudoers file by another user, the first likely culprit is `cybert`. Upon navigating to this users home directory and looking at their bash history, it can be seen that they had ran `sudo visudo` previously. This is the command to edit the `/etc/sudoers` file. Since elevated privileges are needed to run visudo, there should be a record of authentication in the logs.

3. Check authentication log for file update
   ```
   cd /var/log
   grep visudo auth.log.1
   ```
   Upon moving into the `/var/log` directory and using `grep` to find any entries related to `visudo`, file `auth.log` yielded no results but `auth.log.1` did. The output gave back two results, both running the command `/usr/sbin/visudo`. The difference between these two entries however was the user who ran them. One was run by user `ubuntu` and the other `cybert`. Recall from earlier that user `cybert` was confirmed to have added a user, so this entry is what im looking for. The timestamp for this entry is `Dec 28 06:27:34` which was accepted as the answer.

#### Answer
* `Dec 28 06:27:34`