# Windows Subsystem for Linux

Now you can access the power of both Windows and Linux at the same time on a Windows machine. The Windows Subsystem for Linux (WSL) lets you install a Linux distribution (such as Ubuntu, OpenSUSE, Kali, Debian, Arch Linux, etc) and use Linux applications, utilities, and Bash command-line tools directly on Windows, unmodified, without the overhead of a traditional virtual machine or dualboot setup.

## Prerequisites

You must be running Windows 10 version 2004 and higher (Build 19041 and higher) or Windows 11 to use the commands below.

Open "**Winver**" in Run Utility (Win+R)

## Install WSL command

You can now install everything you need to run WSL with a single command. Open PowerShell or Windows Command Prompt in **administrator** mode by right-clicking and selecting "Run as administrator", enter the `wsl --install --no-distribution` command, then restart your machine.

This command will enable the features necessary to run WSL

Now use this `wsl --list --online` command to find list of available Distributions of Linux then Run `wsl --install -d <DistroName>` to install a distro.

In my case it's 

```powershell
wsl --install -d Ubuntu-22.04
```

You just need to install either LTS or any recent version of ubuntu.

Example Username `cyberalliance`

Example Password `tq*!YaXB`

After that you should see,
Password updated successfully
Installation successfull!

## Update and upgrade packages

To run a command as administrator (user "root"), use "sudo ".

See "man sudo_root" for details.

Update and upgrade packages

We recommend that you regularly update and upgrade your packages using the preferred package manager for the distribution. For Ubuntu or Debian, use the command:

```bash
sudo apt update && sudo apt upgrade
```

Windows does not automatically update or upgrade your Linux distribution(s). This is a task that most Linux users prefer to control themselves.

## Basic Ubuntu workflow

In order to create a new directory called `files` we’ll write the following, with `mkdir` being the command and `files` being the argument:

```bash
mkdir files
```

After you run this command, you won’t receive any output other than a new line with a blinking cursor. With this fresh line on your terminal, you are ready for your next command.

As we have not received any concrete feedback about our new directory yet, we’ll use a command to learn more about what is in our present working directory. You can confirm that the new directory is indeed there by listing out the files in the directory, with the `ls` command (signifying “**l**i**s**t”):

```bash
ls
```

You’ll receive output that confirms the `files` directory is there

This gives us general information about what is in our present working directory. If we want to have more details, we can run the `ls` command with what is called a flag. In Linux commands, a **flag** is written with a hyphen `-` and letters, passing additional options (and more arguments) to the command. In our example, we’ll add the `-l` flag, which — when paired with `ls` — denotes that we would like to use the option to use a long listing format with our command.

```bash
ls -l
```

Upon pressing `ENTER`, we’ll receive the following output in our terminal:

```
total 4
drwxr-xr-x 2 cyberalliance cyberalliance 4096 Nov 15 03:16 files
```

Here, there are two lines of output. 
The first line refers to computer memory blocks being allocated to this directory, 
the second line mostly refers to user permissions on the file.

To get a somewhat more human readable output, we can also pass the `-h` or `--human-readable` flag, which will print memory sizes in a human readable format, as below.

Generally, one hyphen `-` refers to single-letter options, and two hyphens `--` refer to options that are written out in words. Note that some options can use both formats. We can build multiple options into a command by chaining flags together, as in `-lh`.

For example, the two commands below deliver the same results even though they are written differently

```bash
ls -lh
```

```bash
ls -l --human-readable
```

Both of these commands will return the following output, similar to the output above but with greater context of the memory blocks:

```
total 4.0K
drwxr-xr-x 2 cyberalliance cyberalliance 4.0K Nov 15 03:16 files
```

The first line of output lets us know that 4K of computer memory is dedicated to the folder. The second line of output has many more details, which we’ll go over in more detail. A general high-level reference of all the information that we’ll cover is indicated in the table below.

| File type | Permissions | Link count | Owner         | Group         | File size | Last modified date | File name |
| --------- | ----------- | ---------- | ------------- | ------------- | --------- | ------------------ | --------- |
| d         | rwxr-xr-x   | 2          | cyberalliance | cyberalliance | 4.0K      | Nov 13 18:06       | files     |

You’ll note that the name of our directory, `files`, is at the end of the second line of output. This name indicates which specific item in the `/home/cyberalliance` user directory is being described by the line of output. If we had another file in the directory, we would have another line of output with details on that file.

```
total 8.0K
drwxr-xr-x 2 cyberalliance cyberalliance 4.0K Nov 15 03:16 files
drwxr-xr-x 3 cyberalliance cyberalliance 4.0K Nov 15 03:24 files2
```

At the front of the line, there is a list of characters and dashes. Let’s break down the meaning of each of the characters:

| Character | Description                                                                                                                                                                   |
| --------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| d         | **d**irectory (or folder) — a type of file that can hold other files, useful for organizing a file system; if this were `-` instead, this would refer to a non-directory file |
| r         | **r**ead — permission to open and read a file, or list the contents of a directory                                                                                            |
| w         | **w**rite — permission to modify the content of a file; and to add, remove, rename files in a directory                                                                       |
| x         | e**x**ecute — permission to run a file that is a program, or to enter and access files within a directory                                                                     |

Now we will move onto navigating the file system on our Linux terminal.

We have made a new directory, but we are still in the main `/home/cyberalliance` user directory. In order to move into the `cyberalliance/files` directory that we have created, we’ll use the `cd` command and pass the name of the directory we want to move into as the argument. The command `cd` stands for “**c**hange **d**irectory,” and we’ll construct it like so:

```bash
cd files
```

again, you won’t receive output other than a new line with a blinking cursor, but we can check that we are in the `/home/cyberalliance/files` directory with the `pwd` command:

```bash
pwd
```

You’ll get the following output, confirming where you are:

```
/home/cyberalliance/files
```

This validates that you are in the `/home/cyberalliance/files` directory of thecyberallianceme/cyberalliance` user directory. Does this syntax look familiar to you? It may remind you of a website’s URL with its forward slashes, and, indeed, websites are structured on servers within directories, too.

Let’s move to the primary directory of the server. Regardless of where we are in a filesystem, we can always use the command `cd /` to move to the primary directory:

```bash
cd /
```

To confirm that we have moved and learn what is in this directory, let’s run our list command:

```bash
ls
```

We’ll receive the following output:

```
bin   dev  home  lib    lib64   lost+found  mnt  proc  run   snap  sys  usr
boot  etc  init  lib32  libx32  media       opt  root  sbin  srv   tmp  var
```

There are a lot of files in there! The `/` directory is the main directory of a Linux server, referred to as the “root” directory. Note that the root directory is different from the default “root” user. You can think of the `/` directory as the major artery of a Linux machine, as it contains all the folders necessary to run the computer. For example, the `sys` directory holds the Linux kernel and system information virtual filesystem. If you would like to learn more about each of these directories, you can visit the [Linux Foundation documentation](https://refspecs.linuxfoundation.org/FHS_3.0/fhs-3.0.html).

You’ll also notice that there is a directory we have been in already, the `/home` user folder. From the `/` directory, we can change directories back into `/home` then back into `files`, or we can move directly back into that folder by typing the absolute path there with `cd`:

```bash
cd /home/cyberalliance/files
```

Now, if you run `pwd` you’ll receive `/home/cyberalliance/files` as your output.

A **file path** is the representation of where a file or directory is located on your computer or server. You can call a path to a file or directory in either a relative or absolute way. A **relative path** would be when we move to a location relative to our current working directory, like we did when we were already in `/home/cyberalliance/` and then moved into `files/`. An **absolute path** is when we call the direct line to a location, as we did above withcyberallianceme/cyberalliance/files`, showing that we started in the `/` directory, cacyberalliancethecyberallianceme/sammy/` user directory and then the nested `files/` directory.

Additionally, Linux leverages **dot notation** to help users navigate via relative paths. A single `.` stands for the directory you are currently in, and a double `..` stands for the parent directory. So, from where we currently are (`/home/cyberalliance/files`), we can use two dots to return to the parentcyberallianceme/cyberalliance` user directory, like so:

```bash
cd ..
```

If you run `pwd`, you’ll receive `/home/cyberalliance` as your output, and if you run `ls`, you’ll receive `files` as your output.

Another important symbol to be familiar with is `~` which stands for the home directory of your machine. Here, our home directory is called `/home/cyberalliance` cyberalliancehe sammy user, but on a local machine it may be your cyberallianceame as in `sammy-shark/`.

You can type the following from anywhere on your machine and return to this home directory:

```bash
cd ~
```

Now let's go back to WSL Topics real quick here

## Check which version of WSL you are running

You can list your installed Linux distributions and check the version of WSL each is set to by entering the command: `wsl -l -v` in PowerShell or Windows Command Prompt.

To set the default version to WSL 1 or WSL 2 when a new Linux distribution is installed, use the command: `wsl --set-default-version <Version#>`, replacing `<Version#>` with either 1 or 2.

Learn more in the guide to [Basic commands for WSL](https://learn.microsoft.com/en-us/windows/wsl/basic-commands).

## Enable Virtual Machine feature

```powershell
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

## Linux kernel update package

The Linux kernel update package installs the most recent version of the [WSL 2 Linux kernel](https://github.com/microsoft/WSL2-Linux-Kernel) for running WSL inside the Windows operating system image.

Download the latest package:

- [WSL2 Linux kernel update package for x64 machines](https://wslstorestorage.blob.core.windows.net/wslblob/wsl_update_x64.msi)

Run the update package downloaded in the previous step. (Double-click to run - you will be prompted for elevated permissions, select ‘yes’ to approve this installation.)

# 
