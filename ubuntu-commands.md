Signing as root

`sudo -s`

- `sudo apt update`: Fetches the list of available updates
- `sudo apt upgrade`: Strictly upgrades the current packages
- `sudo apt full-upgrade`: Installs updates ([add or remove packages](https://askubuntu.com/a/1398989/349837)), [equivalent of dist-upgrade](https://askubuntu.com/a/770140/349837)

Adding a Non root user
`sudo useradd -u 1000 -g 1000 username`

`sudo passwd username`

Check user ID for a Username
`id -u username`

Deleting user

`sudo userdel username`

Deleting user with it's home direcotry

`sudo userdel -r username`

Check user permissions for a file/directory

`ls -l filename`
You can also use the namei -m command followed by the file or directory path to output all of the permissions in the path in a vertical list

`namei -m /path/to/file`

List all users on ubuntu

`compgen -u`

Change folder ownership to a certain user

`sudo chown -R username:username /path/to/folder`
