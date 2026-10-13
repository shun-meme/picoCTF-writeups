# plumbing

**Category:** General Skills

**Difficulty:** Medium

## Description

> Sometimes you need to handle process data outside of a file.
> Can you find a way to keep the output from this program and search for the flag?

## Hints 

1. Remember the flag format is academy{XXXX}.
2. What's a pipe? No not that kind of pipe... This [kind](https://www.linfo.org/pipes.html).

## Files Provided

- None (netcat challenge instance)

--- 

## Solutions

### 1. Initial Recon 

- After launching the instance, a new instruction was provided: 
```text
Connect to xebec.cylabacademy.net 45012(port number changes with instance).
```

- I connected to the provided server with netcat: 
```bash
nc xebec.cylabacademy.net 45012
```

- As soon as I ran the command above, thousands of text lines were printed, so I stopped with `CTRL+C`.

### 2. Key Observations

- The hints mentioned `piping` and the `flag format: academy{xxx}`.

- The hints indicated that I can [grep](https://www.linfo.org/grep.html) the flag from the output by [piping](https://www.linfo.org/pipes.html).

### 3. Solving Steps

- I ran the command below:
```bash 
nc xebec.cylabacademy.net 45012 | grep academy{
```

- And the output was: 
```text
academy{***} [redacted]
```

## Flag

<details>
<summary>Click here to reveal flag</summary>

```text
academy{digital_plumb3r_CB83CD6b}
```

</details>

## Lessons Learned

- `nc` (netcat) opens a raw TCP connection and streams whatever bytes the server sends — no protocol handshake.
