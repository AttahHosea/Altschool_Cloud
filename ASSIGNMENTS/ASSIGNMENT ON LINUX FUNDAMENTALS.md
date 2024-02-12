# LINUX FUNDAMENTALS

## PROBLEM
Your login name: altschool i.e., home directory /home/altschool. The home directory contains the following sub-directories: code, tests, personal, misc Unless otherwise specified, you are running commands from the home directory.

a.Change directory to the tests directory using absolute pathname

b.Change directory to the tests directory using relative pathname

c.Use echo command to create a file named fileA with text content ‘Hello A’ in the misc directory

d.Create an empty file named fileB in the misc directory. Populate the file with a dummy content afterwards

e.Copy contents of fileA into fileC

f.Move contents of fileB into fileD

g.Create a tar archive called misc.tar for the contents of misc directory

h.Compress the tar archive to create a misc.tar.gz file

I. Create a user and force the user to change his/her password upon login

J. Lock a users password

K. Create a user with no login shell

L. Disable password based authentication for ssh

M. Disable root login for ssh

Mode of submission:

you are going to push the required commands to your github repositories.

Deadline: 10th Feb 2024

## SOLUTION

1. `Change directory to the tests directory using absolute pathname`  
    "cd /home/altschool/tests"
    ![absolute path](images/one.png)

2. `Change directory to the tests directory using relative pathname`  
    "cd ./tests"
    ![relative path](images/two.png)

3. `Use echo command to create a file named fileA with text content Hello A in the misc directory`  
    "echo "Hello A" | sudo tee fileA"
    ![create fileA](images/three.png)

4. `Create an empty file named fileB in the misc directory. Populate the file with a dummy content afterwards`  
    "sudo touch fileB"
    "echo "I present to you dummy content" | sudo tee fileB"
    ![create empty file](images/four.png)

5. `Copy contents of fileA into fileC`  
    "sudo cp fileA fileC"
    ![cut fileA](images/five.png)

6. `Move contents of fileB into fileD`  
    "sudo mv fileB fileD"
    ![move fileB](images/six.png)

7. `Create a tar archive called misc.tar for the contents of misc directory`  
    "sudo tar -cvf misc.tar ./misc"
    ![create .tar archive](images/seven.png)

8. `Compress the tar archive to create a misc.tar.gz file`  
    "sudo gzip misc.tar"
    ![compress misc.tar to gz](images/eight.png)

9. `Create a user and force the user to change his/her password upon login`  
    "sudo useradd dummyuser2"
    "sudo passwd --expire dummyuser2"
    ![new user with no passwd](images/nine.png)

10. `Lock a users password`  
    "sudo passwd --lock dummyuser2"
    ![lock user passwd](images/ten.png)

11. `Create a user with no login shell`  
    "sudo adduser --system --no-create-home --shell /usr/bin/nologin dummyuser3"
    ![no login shell](images/eleven.png)

12. `Disable password based authentication for ssh`  
    "sudo nano /etc/ssh/sshd_config"
    "sudo systemctl restart sshd"
    ![disable passwd](images/twelve_thirteen.png)

13. `Disable root login for ssh`  
    "sudo nano /etc/ssh/sshd_config"
    "sudo systemctl restart sshd"
    ![disable root login for ssh](images/twelve_thirteen.png)

## FULLSCREEN
![fullscreen1](images/fs1.png)  ![fullscreen1](images/fs2.png)  ![fullscreen1](images/fs3.png)

## ERROR
While testing a few commands for `problem 8` i ran into an error that made my virtual machine unresponsive. I had to exit my terminal and shutdown virtual machine from the virtual box. Attached below is the error screen and the restart screen.

![fullscreen error](images/error.png)  ![restart screen](images/restart.png)