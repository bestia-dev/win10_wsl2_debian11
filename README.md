[//]: # (auto_md_to_doc_comments segment start A)

# win10_wsl2_debian11

**01. Tutorial to install Linux on Windows. Linux everywhere! (win10_wsl2_debian11) (2022-03)**  
***version: 1.0  date: 2022-09-03 author: [bestia.dev](https://bestia.dev) repository: [GitHub](https://github.com/CRUSTDE-Containerized-Rust-Dev-Env/win10_wsl2_debian11)***  

 ![maintained](https://img.shields.io/badge/maintained-green)
 ![ready_for_use](https://img.shields.io/badge/ready_for_use-green)
 ![tutorial](https://img.shields.io/badge/tutorial-yellow)
 ![win10_wsl2_debian11](https://bestia.dev/webpage_hit_counter/get_svg_image/556625040.svg)

 ![logo](https://raw.githubusercontent.com/CRUSTDE-Containerized-Rust-Dev-Env/CRUSTDE-Containerized-Rust-Dev-Env/main/images/crustde_250x250.png)
 win10_wsl2_debian11 is a member of the [CRUSTDE-Containerized-Rust-Dev-Env](https://github.com/orgs/CRUSTDE-Containerized-Rust-Dev-Env/repositories?q=sort%3Aname-asc) project.

Hashtags: #rustlang #tutorial  
My projects on GitHub are more like a tutorial than a finished product: [bestia-dev tutorials](https://github.com/bestia-dev/tutorials_rust_wasm).

For 30 years of my professional life, I programmed in Windows. It was good.  
I am on a long vacation now and is time to learn something new.  

This project has also a youtube video tutorial. Watch it:
<!-- markdownlint-disable MD033 -->
[<img src="https://bestia.dev/youtube/win10_wsl2_debian11.jpg" width="400px">](https://bestia.dev/youtube/win10_wsl2_debian11.html)
<!-- markdownlint-enable MD033 -->

## Linux everywhere

My conclusion is that Windows (and MacOS) should just die a long death and be replaced by Linux.  
Microsoft obviously concluded the same, therefor they introduced WSL (Windows Subsystem for Linux). Now we can run more and more Linux programs inside Windows. So Windows is less and less interesting to programmers.  
MacOS and iOS are already similar to Linux because they are based on BSD, a cousin of Unix.  
Android is basically a bastard child of Linux and Google.  
Almost all the web servers and servers in the cloud are Linux today.  
So today it makes sense to do all the programming only for Linux.  

## standard modern GUI

The "elephant in the room" is the GUI. Every OS has on purpose made the GUI different and completely incompatible. Sadly!
But we have a strong international standard for GUI that works literally everywhere: it is HTML+CSS+JavascriptEngine.  
I explicitly didn't say Javascript, let's call it by its true name **ECMAScript** because it is an abomination.  
Fortunately, we have now [WebAssembly](https://developer.mozilla.org/en-US/docs/WebAssembly) abbreviated as [WASM](https://webassembly.org/) to save the day.  
We can finally make client programs for the browser in some "normal" programming languages like Rust and many others.

## Win10

Win10 is so ubiquitous that I have nothing interesting to say. It works just fine with all the drivers and peripherals and it comes preinstalled on most of the notebooks. We can say it is a winning OS in the desktop/notebook segment. In the enterprise world, Microsoft still has a firm grip with its Office suite. Blue-collar workers are just hooked to it like drug addicts even when there are good alternatives.  
But Windows lost completely in the server segment and shamefully in the smartphone segment.  
We "must" use it on notebooks because of the drivers, but it is slowly dying.  
I don't have any opinion of Win11. Microsoft "promised" that Win10 was the last version of Windows and that the number will last forever and be free. In the background, there will be minor and major updates. They broke their promise. I think nobody really loves Win11.  
It looks more like they are trying to push people away from Windows on purpose.  

## Installing WSL2  
  
WSL2 is a revolution. With it, I have a lightweight virtual machine with a true Linux kernel. On my Lenovo notebook, I have Win10 and it works fine with all the drivers and peripherals, but now I have also Linux, so I can do some serious programming for the Linux cloud servers. Not just one Linux, I can have multiple Linux OS simultaneously on the same machine because they run in a VM.  
Let's install/enable it on Win10:  
<https://docs.microsoft.com/en-us/windows/wsl/install-win10#update-to-wsl-2>  
Open `PowerShell Run as Administrator`:  

```powershell
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
# restart and update to WSL2
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
# MANDATORY RESTART YOUR MACHINE !
# if not, the wsl --help command will not have the --set-default-version argument !
# Set WSL2 as default
wsl --set-default-version 2
```

I get the error: WSL 2 requires an update to its kernel component.  
Visit <https://aka.ms/wsl2kernel> and do the update.  

```powershell
# I can update the wsl now
wsl --update
# then shutdown the wsl for update to take effect
wsl --shutdown
# 
wsl --list --online
```

## Debian11 - Bullseye

Debian is considered the grandfather of Linux-based operating systems. The Linux OSes are called "distribution" or "distro". All of them have in common the Linux Kernel developed firstly by Linux Torvald, but they differ in other components that make an Operating system.  
Debian is conservative in its release cycle to ensure high stability. Some say that it is boringly stable ;-) I am old and I like "stable".  
Some distros are derived from Debian and share a lot with it. Everybody has heard of Ubuntu, a big Linux popularity success for desktops.  
The new version of Debian is 11. Every version has its unique name, version 11 is called Bullseye. Nice name.  
Use the Microsoft Store to install Debian inside WSL2:  

<https://www.microsoft.com/en-us/p/debian/9msvkqc78pk6>  

or in PowerShell a few lines:

```powershell
# list the distros
wsl --list --online
# install Debian
wsl --install -d Debian
```

It takes a minute! Now we can open the Debian bash terminal using the provided icon or we can type `wsl` or `Debian` in the start menu, command prompt or PowerShell terminal. This Debian is without the GUI desktop. We could additionally install it, but we will rarely need it. A lot of Linux programs for programmers work just fine in the non-GUI mode inside a bash terminal.  
The Windows user is automatically also a Debian user.  

In the bash terminal we can type these commands to update/upgrade Debian packages:  

```bash
sudo apt update
sudo apt -y full-upgrade
cat /etc/debian_version
# 11.4
```

WSL2 works very fast with its own filesystem.  
From Linux, we can access the win10 filesystem mounted on `/mnt/c/`, but this is very slow.  
From Windows, we can access the Linux files on `\\wsl$\Debian\`.  But sometimes when we copy files, we get an additional annoying file "*.attr" for attributes that differ on the 2 filesystems. I always delete it.  

## Removing Debian

If you want a fresh new installation of Debian it is easy to remove the existing one in the `cmd prompt`:

```cmd
# get the exact distro name
wsl -l -v
wsl --unregister Debian
```

## Removing WSL2

If you need to remove WSL2 open `PowerShell Run as Administrator`:

```powershell
Disable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
```

## Read more

Read how I create a complete [
TDE Containerized Rust Development Environment](https://github.com/CRUSTDE-Containerized-Rust-Dev-Env/docker_rust_development) and how I configure and use my [Rust](https://github.com/CRUSTDE-Containerized-Rust-Dev-Env/development_environment) Development Environment](https://github.com/CRUSTDE-Containerized-Rust-Dev-Env/development_environment).  

## Updates 2024 and new knowledge

Debian is now 12 bookworm. But that doesn't change much. It is easy to uninstall the old Debian and install the new one just with the same commands.  
First, store the important configuration of Debian somehow and restore it later.  
The same commands will install the latest version. That takes just a minute! Great!.  

## WSL2: disable automount of Windows drives

My main OS Windows can see the files inside WSL using paths like this: `\\wsl$\Debian\home\` or `\\wsl.localhost\Debian\home\`. I think this is fine. The host can see the guest.

I don't like that programs in WSL can see the files of my host OS Windows. The win drives are mounted like `/mnt/c/`, `/mnt/d/`,... It is called WSL automount. I want to disable that.  
For "security" I don't want WSL to see Windows drives, folders and files by default. It is never good that the guest can see the host. This access is even read/write. Bad.

There is a half-baked solution from Microsoft, but workable for my use case. https://tonym.us/improve-wsl-security-with-read-only-filesystem.html  
A malicious actor could still mount any Windows folder he wants if he gets admin privilege in WSL because then he can change the `/etc/wsl.conf` file.  
This is not a good sandbox. It just makes exploits a little bit trickier, but possible nonetheless.  
https://github.com/microsoft/WSL/issues/7236  
Microsoft always does everything unsafe by default! On purpose. Bad Microsoft!

Write in the Debian file `/etc/wsl.conf`

```conf
# Automatically mount Windows drive when the distribution is launched
[automount]

# disable auto-mounting of win drives
enabled = false

# process fstab entries to allow some folders to be mounted
mountFsTab = true

# disable launching windows exe files
[interop]
enabled = false
appendWindowsPath = false
```

After `wsl --shutdown` and restart, the win drives are not automounted anymore, but the mounting points are still here.  
It is delicate to remove a mounting point. If it is still mounted, it would delete all the data inside. Very bad design.

```bash
$ ls /mnt
c  d  wsl  wslg

# first check 100% that it is not mounted:
$ sudo umount /mnt/c
umount: /mnt/c: not mounted.

# then remove the mount point:
sudo rm -r /mnt/c

# first check 100% that it is not mounted:
$ sudo umount /mnt/d
umount: /mnt/d: not mounted.

# then remove the mount point:
sudo rm -r /mnt/d

# mounting points are now deleted
$ ls /mnt
wsl  wslg
```

Now when starting WSL I get a stupid error:
<3>WSL (9) ERROR: UtilTranslatePathList:2866: Failed to translate C:\Users\luciano
And I don't know from where it comes from.
The appendWindowsPath is already set to false. Usually, this is the main reason for errors like that.  

To be on the super cautious side I will also disable the `virtio9p` protocol that is used by wsl to access the files in windows. At least I hope I understood that right.  

In Windows create the file `~/.wslconfig`

```conf
[wsl2]
# disable wsl from accessing windows files
virtio9p=false
```

## SSH

Install ssh client:

```bash
sudo apt-get install openssh-client
```

## .bashrc

Add these lines to ~/.bashrc to activate ssh-agnet:

```bash

# Luciano 2024-03-19: I added some commands for my configuration of Debian ( in WSL2 on Windows)
# ~/.bashrc is executed by bash for non-login interactive shells every time.  (not for login non-interactive scripts)
# Append to ~/.bashrc
# Then if you don't want to restart the terminal and use immediately, run
# source ~/.bashrc
# I tried to add this to ~/.bash_profile, but it didn't work well.

# alias for the very often used command ls
alias l="ls -al"
alias ll="ls -l"

# Added to bashrc for easy sshadd and postgres
export PATH=$HOME/bin:$PATH

# disable XON/XOFF flow control and ctrl-s
stty -ixon
bind -r "\C-s"  
# disabel ctrl-b, because I want VSCode to use it.
bind -r "\C-b"  

# region: ssha-agent and ssh-add

SSH_ENV="$HOME/.ssh/agent-environment"

function start_agent {
    /usr/bin/ssh-agent | sed 's/^echo/#echo/' > "${SSH_ENV}"
    chmod 600 "${SSH_ENV}"
    . "${SSH_ENV}" > /dev/null
    /usr/bin/ssh-add;
}

# Source SSH settings, if applicable
if [ -f "${SSH_ENV}" ]; then
    . "${SSH_ENV}" > /dev/null
    ps -ef | grep ${SSH_AGENT_PID} | grep ssh-agent$ > /dev/null || {
        start_agent;
    }
else
    start_agent;
fi

echo "Use the global command 'sshadd' to simply add your private SSH keys to ssh-agent $SSH_AGENT_PID."
alias sshadd="echo sh ~/.ssh/sshadd.sh; sh ~/.ssh/sshadd.sh"

# region: ssha-agent and ssh-add
```

## sshadd

To make it easier to add ssh keys to ssh-agent put this script in ~/.ssh/sshadd.sh.  
The alias `sshadd` is already in ~/.bashrc.  

```bash
#!/bin/sh

# ~/.ssh/sshadd.sh
# Inside this template, replace the words github_com_git_ssh_1 and bestia_dev_luciano_bestia_ssh_1 
# with your identity file names for the ssh private key.

echo "  \033[33m Add often used SSH identity private keys to ssh-agent \033[0m"
echo " "
echo "  \033[33m The ssh-agent should be started already on login inside the ~/.bashrc script. \033[0m"
echo "  \033[33m <https://github.com/CRUSTDE-Containerized-Rust-Dev-Env/docker_rust_development/blob/main/ssh_easy.md> \033[0m"
echo "  \033[33m It is recommended to use the ~/.ssh/config file to assign explicitly one ssh key to one ssh server. \033[0m"
echo "  \033[33m If not, ssh-agent will send all the keys to the server and the server could refute the connection because of too many bad keys. \033[0m"

# check the content of ~/.ssh/config if it contains the ssh keys
cat ~/.ssh/config | grep -q "~/.ssh/github_com_git_ssh_1" || echo "The ~/.ssh/config does not contain the identity ~/.ssh/github_com_git_ssh_1."
cat ~/.ssh/config | grep -q "~/.ssh/bestia_dev_luciano_bestia_ssh_1" || echo "The ~/.ssh/config does not contain the identity ~/.ssh/bestia_dev_luciano_bestia_ssh_1."

# add if key not yet exist in ssh-agent for git@github.com
ssh-add -l | grep -q `ssh-keygen -lf ~/.ssh/github_com_git_ssh_1 | awk '{print $2}'` || ssh-add -t 1h ~/.ssh/github_com_git_ssh_1

# add if key not yet exist in ssh-agent for luciano_bestia@bestia.dev
ssh-add -l | grep -q `ssh-keygen -lf ~/.ssh/bestia_dev_luciano_bestia_ssh_1 | awk '{print $2}'` || ssh-add -t 1h ~/.ssh/bestia_dev_luciano_bestia_ssh_1

echo "  \033[33m The keys are set to expire in 1 hour. \033[0m"
echo "  \033[33m For security, when you are finished using the keys, remove them from the ssh-agent with: \033[0m"
echo "\033[32mssh-add -D \033[0m"
echo " " 
echo "   \033[33m List public fingerprints inside ssh-agent: \033[0m"
echo "\033[32mssh-add -l \033[0m"
ssh-add -l

echo " "

```

## Quirks

### network connection after sleep

After putting the laptop to sleep, sometimes the WSL2 does not work right. When I need to use `localhost` or `127.0.0.1` connection from Win10 to a Linux program, the connection is broken. I have to restart the WSL in `PowerShell Run as administrator` with  
`Get-Service LxssManager | Restart-Service`.  
Not nice and very difficult to discover because WSL2 is running just fine, except for this.  

### external disk obsolete content

Sometimes the content of an external disk is completely wrong when looked at from the WSL2. It is obsolete, something that is a remnant of other external disks. I think I unmounted the `mnt/d` in Linux and then mount it back to solve the problem.  

### git repository corruption

My git repository inside WSL2 got corrupted. It looks that this happens to many people on WSL2.  
The cure is:  

```batch
# backup the repo first!
find .git/objects/ -type f -empty | xargs rm
git fetch -p
git fsck --full
```

## Open-source and free as a beer

My open-source projects are free as a beer (MIT license).  
I just love programming.  
But I need also to drink. If you find my projects and tutorials helpful, please buy me a beer by donating to my [PayPal](https://paypal.me/LucianoBestia).  
You know the price of a beer in your local bar ;-)  
So I can drink a free beer for your health :-)  
[Na zdravje!](https://translate.google.com/?hl=en&sl=sl&tl=en&text=Na%20zdravje&op=translate) [Alla salute!](https://dictionary.cambridge.org/dictionary/italian-english/alla-salute) [Prost!](https://dictionary.cambridge.org/dictionary/german-english/prost) [Nazdravlje!](https://matadornetwork.com/nights/how-to-say-cheers-in-50-languages/) 🍻

[//bestia.dev](https://bestia.dev)  
[//github.com/bestia-dev](https://github.com/bestia-dev)  
[//bestiadev.substack.com](https://bestiadev.substack.com)  
[//youtube.com/@bestia-dev-tutorials](https://youtube.com/@bestia-dev-tutorials)  

[//]: # (auto_md_to_doc_comments segment end A)
