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

### Question: 
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

### Question: 
What was the present working directory (PWD) when the previous command was run?

#### Process
   1. The present working directory can be found through following the same steps from step 2 from the question before as the output of ```grep sudo auth.log.1 | grep dokuwiki``` also contains the directory where the command was executed. Therefore, answering the previous question answers this question as well.  The log entry shows the working directory as: ```PWD=/home/cybert```.

#### Answer
* `/home/cybert` 