# Magikarp Ground Mission

**Category:** General Skills

**Difficulty:** Easy 

## Description

> Do you know how to move between directories and read files in the shell?<br>
> Start the container, ssh to it, and then ls once connected to begin.

## Hints 

1. Finding a cheatsheet for bash would be really helpful!

## Files Provided

- None (SSH challenge instance)

--- 

## Solutions

### 1. Initial Recon 

- Launched the instance, and connected via SSH using the provided credentials.

### 2. Key Observations

- Firstly: 

 ```bash
ls -la 
```

- Saw the files `1of3.flag.txt instructions-to-2of3.txt` 

```bash
cat 1of3.flag.txt
```

- Output: 

```txt
academy{*** [redacted]
```

- Next run: 

```bash
cat instructions-to-2of3.txt 
```

- Output: 

```txt
Next, go to the root of all things, more succinctly `/`
```

- This is when I realised it's solvable by following instructions.txt.

### 3. Solving Steps

- Go to root directory with: 

```bash
cd / 
ls -la 

cat 2of3.flag.txt 
```

- Output: 

```txt
***_**_***_  [redacted] 
```

- And run: 

```bash
cat instructions-to-3of3.txt 
```

- Output: 

```txt
Lastly, ctf-player, go home... more succinctly `~`
```

- Go to home directory with: 

```bash
cd 
```

or 

```bash
cd ~
```

- And: 

```bash
cat 3of3.flag.txt 
```

- Output: 

```txt
***} [redacted] 
```

## Flag

<details>
<summary>Click here to reveal flag</summary>

```txt
academy{xxsh_0ut_0f_//4t3r_47c47679}
  ```

</details>

## Lessons Learned

- always check what files exist in your directories with `ls -la` 
