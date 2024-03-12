Working in GitBash, I downloaded the Ubuntu image using: docker pull ubuntu. 
After that, I did the following:
- created and started running the container by using: winpty docker run -it --name my_linux_container ubuntu.
- added the user named john: adduser john
- copied the file I received into the Linux container: docker cp C:/Users/Cristi/Desktop/tremend/create_large_file.sh my_linux_container:/home/john.
- modified the typo in the file (got the error: 'mv: cannot stat 'lage_file': No such file or directory') with
  sed -i 's/mv lage_file/mv large_file/' create_large_file.sh
- ran the script: ./create_large_file.sh

The commands for the new script:

1. Print the home directory
echo $HOME
2. List all usernames from the passwd file
cut -d: -f1 /etc/passwd
3. Count the number of users
cut -d: -f1 /etc/passwd | sort | uniq | wc -l
4. Find the home directory of a specific user (prompt to enter the username value)
read -p "Enter username: " username
grep "^$username:" /etc/passwd | cut -d: -f6
5. List users with specific UID range (e.g. 1000-1010)
getent passwd | awk -F: -v min="$1000" -v max="$1010" '$3 >= min && $3 <= max {print $1}'
6. Find users with standard shells like /bin/bash or /bin/sh
getent passwd | grep -E '/bin/(bash|sh)$' | cut -d: -f1
7. Replace the “/” character with “\” character in the entire /etc/passwd file and redirect the
content to a new file
sed 's/\//\\/g' /etc/passwd > new_passwd.txt
8. Print the private IP
hostname -I | cut -d' ' -f1
9. Print the public IP
curl ipinfo.io/ip
10. Switch to john user
su john
11. Print the home directory
echo $HOME

I wanted to make a separate file in which I write all the commands, as well as at the beggining read and verify that the 'passwd' file name is correct before actually executing them.
However, I couldn't use any commands, not even sudo, apt, apk, etc. and I didn't have time to properly troubleshoot and solve the problem.