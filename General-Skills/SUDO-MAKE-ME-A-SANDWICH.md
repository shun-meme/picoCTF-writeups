# SUDO MAKE ME A SANDWICH

**Category:** General Skills

**Difficulty:** Easy

## Description

> Can you read the flag?<br>
> I think you can!

## Hints 

1. What is sudo?
2. How do you know what permission you have?

## Files Provided

- None (SSH challenge instance)

---

## Solution

### 1. Initial Recon 

- Launched the instance. 
- Connected via SSH using the provided credentials.

```bash
ls -la 
``` 

- Saw the file 'flag.txt' owned by root.
- Tried reading it:

```bash
cat flag.txt #Permission denied
```

- Tried with sudo: 

```bash
sudo cat flag.txt #failed, asked for sudo password which is not provided 
```

### 2. Key Observations

```bash
sudo -l 
#User ctf-player may run the following commands on challenge:
#    (ALL) NOPASSWD: /bin/emacs
```
indicating i can run 'sudo /bin/emacs' without a password. 

### 3. Solving Steps

- My terminal (kitty) uses a custom TERM variable (xterm-kitty) that the remote server doesn't recognize, so I fixed with: 

```bash
export TERM=xterm 
```

- after that, I opened the file with: 

```bash
sudo /bin/emacs flag.txt 
```
The flag is displayed inside the file.

## Flag 

<details>
<summary>Click here to reveal flag</summary>
  academy{ju57_5ud0_17_101e25fb}
</details>

## Lessons Learned 

- Always run 'sudo -l' to check what privileged commands you're allowed to use.
- Seemingly harmless programs (like text editors) can lead to privilege escalation if they can run as root.
