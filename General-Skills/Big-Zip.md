# Big Zip

**Category:** General Skills
**Difficulty:** Easy

## Description

> Unzip this archive and find the flag.

## Hints 

1. Can grep be instructed to look at every file in a directory and its subdirectories?

## Files Provided

- `big-zip-files.zip`

--- 

## Solutions

### 1. Initial Recon 

- I downloaded the provided zip file and unzipped it:

```bash 
unzip big-zip-files.zip
```

- The unzipped folder `big-zip-files` contained a lot of text files + folders making it unrealistic to go through every file for the flag.

### 2. Key Observations

- I first tried:

```bash
grep -o academy 
``` 
but the command appeared to hang with no output, so I interrupted it with Ctrl+C
w
```

### 3. Solving Steps

- 

## FLag

<details>
<summary>Click here to reveal flag</summary>
</details>

## Lessons Learned

- 

