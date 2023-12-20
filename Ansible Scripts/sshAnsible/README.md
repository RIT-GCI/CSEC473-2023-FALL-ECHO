Author: Travis Hill
Email: twh9811@rit.edu
Date: 9/10/23

Initial Setup:
0.) Some modules required use the community collection in Ansible, depending on how you installed Ansible it may already be there. Either way, run "ansible-galaxy collection install community.general" to ensure that the proper modules are installed.
1.) Have a sudo user that is NOT root on the target host machine and connect to that user in the ansible hosts file. I.e. instead of 10.13.58.242 you put sudoUser@10.13.58.242
2.) Generate an SSH key for the root user on the control ansible node with all empty parameters.
3.) Copy SSH key from control node to target host machine by using the command: ssh-copy-id "sudoUserHere@hostIPHere"
4.) Run ansible-playbooks with the -K flag set. When prompted, enter the target machines root password.

Make sure to modify the hosts file to fit deployment needs and to modify the username variable where needed as well.

IMPORTANT NOTE:
For some unknown reason when you SSH in to the target machine, it may ask for the password still despite all the options being turned off.  Why? I couldn't figure it out. I installed from scratch multiple times with the same exact setup, following the same exact instructions/process and it was recreated sometimes othertimes it wasn't and worked as intended.
If this does happen to you delete all .ssh folders for the involved users, run "sudo apt-get remove --purge openssh-server" to clear the config changes and reinstall it with default settings using "sudo apt-get install openssh-server". Repeat initial setup and this process until it works.
