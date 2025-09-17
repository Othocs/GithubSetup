---
title: GitHub Setup Guide
layout: default
---


Here is a simple guide to follow if you want to setup github for the first time on your MAC 

Github and you MAC are connected using SSH Keys, first let's check if you have any. If not we will generate one.
# Check if you already have an SSH Key in the terminal:

```shell
ls -al ~/.ssh
```

Example of what you should see if you already have an ssh key 
```shell
➜  ~ ls -al ~/.ssh
-rw-------@  1 othocs  staff   464 Aug 19 21:27 id_ed25519
-rw-r--r--@  1 othocs  staff   106 Aug 19 21:27 id_ed25519.pub
```

You should look for filenames of this format (SSH Keys format):
- _id_rsa.pub_
- _id_ecdsa.pub_
- _id_ed25519.pub_

If you don't see any file of this format, that means you **DON'T** have an SSH Key.
No worries ! Let's generate one ! 

---
# 1: Generate an SSH Key in the terminal

Use this command in the terminal and use your own email:

PS : the  `"your_email@example.com"` is **just a comment/label**  used to easily identify this ssh key in the future. **The email you enter won't have any impact on functionality**

```shell
ssh-keygen -t ed25519 -C "your_email@example.com"
```

## Here’s what would happen step by step:

A) **It will ask for a file path** to save the key (default is `~/.ssh/id_ed25519`):  
**JUST PRESS ENTER TO USE THE DEFAULT LOCATION**

```shell
> Enter a file in which to save the key (/Users/YOU/.ssh/id_ALGORITHM): [Press enter]
```

B) It will ask for an optional passphrase (VERY RECOMMENDED):
You can set here a password to secure the use of your SSH Key.
It is recommended, but make sure to enter a password you'll remember because it's very hard to recover.

```shell
Copy code
> Enter passphrase (empty for no passphrase): [Type a passphrase]
> Enter same passphrase again: [Type passphrase again]
```

# 2: Adding the SSH Key to the SSH-Agent

`ssh-agent` securely stores your private key in memory after you unlock it once, so you don’t have to re-enter your passphrase every time.  
It also automatically supplies the right key when you connect, making SSH/Git operations seamless and faster.

### A) **Start the ssh-agent in the background.**

```shell
eval "$(ssh-agent -s)"
```
You should see this : 
```shell
> Agent pid 59566
```

### B) **Check to see if your `~/.ssh/config` file exists in the default location.**
```shell
open ~/.ssh/config
```

If you see this :
```shell
> The file /Users/YOU/.ssh/config does not exist.
```
That means the file does not exist so we need to create it with this simple command : 
```shell
touch ~/.ssh/config
```

### C) ** Configure SSH to Use Your Key**

1. First, **check what your SSH key file is actually called**:
    
    ```bash
    ls ~/.ssh/
    ```
    
    Look for a file starting with `id_` (e.g., `id_ed25519`, `id_rsa`).  
    That’s the private key you’ll want to use.
    
2. Open or create the SSH config file:
    
    ```bash
    open ~/.ssh/config
    ```
    
3. Add these lines (replace `id_ed25519` with the correct filename if yours is different):
    
    ```
    Host github.com
      AddKeysToAgent yes
      UseKeychain yes
      IdentityFile ~/.ssh/id_ed25519
    ```
    
4. Save and close the file.
    

> **Note**  
> 
> - If you chose not to add a passphrase to your key, you should omit the `UseKeychain` line.  
> - If you see a `Bad configuration option: usekeychain` error, add an additional line to the configuration's `Host *.github.com` section.  
> 
> ```text
> Host github.com
>   IgnoreUnknown UseKeychain
> ```

### D) Add SSH Key to the ssh-agent

Add your SSH private key to the ssh-agent and store your passphrase in the keychain. Like before, make sure to put the correct ssh key name (check step C if you don't remember)

```shell
ssh-add --apple-use-keychain ~/.ssh/id_ed25519
```

> **Note**  
> The `--apple-use-keychain` option stores the passphrase in your keychain for you when you add an SSH key to the ssh-agent.  
> If you chose not to add a passphrase to your key, run the command without the `--apple-use-keychain` option.


---

# FINAL STEP : Adding the ssh key to github

Congratulations ! Only one thing left to do and you will be setup to use github ! 

### 1: Copy the SSH key to the clipboard

If your SSH public key file has a different name than the example code, modify the filename to match your current setup.

```shell
pbcopy < ~/.ssh/id_ed25519.pub
```

### 2: Go to your github settings on the github website
![GitHub settings navigation](./Pasted%20image%2020250917135257.png)
![SSH keys section](./Pasted%20image%2020250917135442.png)
![Add new SSH key](./Pasted%20image%2020250917135546.png)

Add the SSH Key and you should be good to go !

---
# Test that the ssh Connection works

Here’s the content from your screenshot turned into nicely formatted Markdown:


```shell
ssh -T git@github.com
```

You may see a warning like this:

```
> The authenticity of host 'github.com (IP ADDRESS)' can't be established.
> ED25519 key fingerprint is SHA256:+DiY3wvvV6TuJJhbpZisF/zLDA0zPMSvHdkr4UvCOqU.
> Are you sure you want to continue connecting (yes/no)?
```

3. Verify that the fingerprint in the message you see matches [GitHub's public key fingerprint](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/githubs-ssh-key-fingerprints) if it does, then type `yes`:

```
> Hi USERNAME! You've successfully authenticated, but GitHub does not
> provide shell access.
```

**The ssh connection should be good to be used now**

