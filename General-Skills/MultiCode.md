# MultiCode

**Category:** General Skills

**Difficulty:** Easy 

## Description

> We intercepted a suspiciously encoded message, but it’s clearly hiding a flag. No encryption, just multiple layers of obfuscation. Can you peel back the layers and reveal the truth? Download the `message`.

## Hints 

1. The flag has been wrapped in several layers of common encodings such as ROT13, URL encoding, Hex, and Base64. Can you figure out the order to peel them back?
2. A tool like [CyberChef](https://cyberchef.org/) can be interesting. 

## Files Provided

- `message.txt`

--- 

## Solutions

### 1. Initial Recon 

- I downloaded the file and viewed its contents with `cat message.txt`

- Output: 
```text
NmU3MDZlNzE3MjdhNmMyNTM3NDI2MTcyNjY2NzcyNzE1ZjcyNjE3MDMwNzE3NjYxNzQ1ZjM2NzIzNDM5NmUzODM3MzkyNTM3NDQ=
```

- I was new to encodings, but I figured I'd need to put this output into [CyberChef](https://cyberchef.org/) until I got the flag. 

### 2. Key Observations

- As mentioned in the first hint, I would need to apply ROT13, URL encoding, Hex, and Base64 operations in the correct order.

### 3. Solving Steps

- First, I pasted the following into the input:
```text
NmU3MDZlNzE3MjdhNmMyNTM3NDI2MTcyNjY2NzcyNzE1ZjcyNjE3MDMwNzE3NjYxNzQ1ZjM2NzIzNDM5NmUzODM3MzkyNTM3NDQ=
```

- For the operation, I chose `From Base64` since the string ends with a `=`.

- The output changed to:
```text
6e706e71727a6c2537426172666772715f72617030717661745f367234396e383739253744
```

- Next, I used the `From Hex` operation and the output was:
```text
npnqrzl%7Barfgrq_rap0qvat_6r49n879%7D
```

- Then I added the `URL Decode` operation and got the output below:
```text
npnqrzl{arfgrq_rap0qvat_6r49n879}
```

- Lastly, I used the `ROT13` operation and the final output was:
```text
academy{***} [redacted]
```

## Flag

<details>
<summary>Click here to reveal flag</summary>

```text
academy{nested_enc0ding_6e49a879}
```

</details>

## Lessons Learned

- What encoding is, and how it differs from encryption.
- How to recognize common encoding formats by their visual signatures (e.g., `=` ending for Base64, only `0-9a-f` for Hex, `%xx` for URL encoding, shifted letters for ROT13)
- Which [CyberChef](https://cyberchef.org/) operation to use once I identify the format

