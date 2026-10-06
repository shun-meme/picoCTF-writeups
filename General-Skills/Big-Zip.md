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

## Solution

### 1. Initial Recon 

- I downloaded the provided zip file and unzipped it:

```bash 
unzip big-zip-files.zip
```

- The unzipped folder `big-zip-files` contained a lot of text files + folders making it unrealistic to go through every file for the flag.

### 2. Key Observations

- I first tried `grep -o academy`, but the command appeared to hang with no output, so I interrupted it with Ctrl+C.

### 3. Solving Steps

- Next I tried `grep -ro academy`, which returned a single file path. 

```text
folder_pmbymkjcya/folder_cawigcwvgv/folder_ltdayfmktr/folder_fnpfclfyee/whzxrpivpqld.txt:academy
```

- Now that I knew which file contained the flag, I viewed its contents with: 

```bash
cat folder_pmbymkjcya/folder_cawigcwvgv/folder_ltdayfmktr/folder_fnpfclfyee/whzxrpivpqld.txt
```

- And the output was: 

```text
information on the record will last a billion years. Genes and brains and books encode academy{***} [redacted]
```

## Flag

<details>
<summary>Click here to reveal flag</summary>

```text
academy{gr3p_15_m4g1c_ef8790dc}
```

</details>

## Lessons Learned

- `grep -r` is essential for recursive search.
- Without `-r` or a file argument, grep reads stdin and hangs. 
- `-o` only prints the matched portion.

