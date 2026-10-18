# bytemancy 2

**Category:** General Skills 

**Difficulty:** Medium

## Description

> Can you conjure the right bytes?
> The program's source code can be downloaded [here](https://challenge-files.cylabacademy.net/library/53cac0b2b4e932293c13dd3d0144509deeb0970d7e9117ef59f20d030c312edc/app.py)

## Hints 

1. There's no way to print these bytes.
2. Use [pwntools](https://docs.pwntools.com/en/stable/) to send raw bytes over the network.

## Files Provided

- nc address + port (netcat challenge instance)
- [app.py](https://challenge-files.cylabacademy.net/library/53cac0b2b4e932293c13dd3d0144509deeb0970d7e9117ef59f20d030c312edc/app.py)

--- 

## Solutions

### 1. Initial Recon 

- After launching the instance, it showed the address and the port number to connect with `netcat (nc)`
- The output was:
```text 
⊹──────[ BYTEMANCY-2 ]──────⊹
☍⟐☉⟊☽☈⟁⧋⟡☍⟐☉⟊☽☈⟁⧋⟡☍⟐☉⟊☽☈⟁⧋⟡☍⟐

Send me the HEX BYTE 0xFF 3 times, side-by-side, no space.

☍⟐☉⟊☽☈⟁⧋⟡☍⟐☉⟊☽☈⟁⧋⟡☍⟐☉⟊☽☈⟁⧋⟡☍⟐
⊹─────────────⟡─────────────⊹
==> 
```
- Whatever I typed, it returned `That wasn't it. I got: b'[whatever I typed]'`

- This below is the content of the provided `app.py`(collapsed): 
<details>

```py 
import sys

while(True):
  try:
    print('⊹──────[ BYTEMANCY-2 ]──────⊹')
    print("☍⟐☉⟊☽☈⟁⧋⟡☍⟐☉⟊☽☈⟁⧋⟡☍⟐☉⟊☽☈⟁⧋⟡☍⟐")
    print()
    print('Send me the HEX BYTE 0xFF 3 times, side-by-side, no space.')
    print()
    print("☍⟐☉⟊☽☈⟁⧋⟡☍⟐☉⟊☽☈⟁⧋⟡☍⟐☉⟊☽☈⟁⧋⟡☍⟐")
    print('⊹─────────────⟡─────────────⊹')
    print('==> ', end='', flush=True)
    user_input = sys.stdin.buffer.readline().rstrip(b"\n")
    if user_input == b"\xff\xff\xff":
      print(open("./flag.txt", "r").read())
      break
    else:
      print("That wasn't it. I got: " + str(user_input))
      print()
      print()
      print()
  except Exception as e:
    print(e)
    break
```
</details>

### 2. Key Observations

- The line `if user_input == b"\xff\xff\xff":` indicates that it wanted me to send this `"\xff\xff\xff"` in order to print the flag.

- Without thinking much, I typed `\xff\xff\xff` into the input but it returned the same: `That wasn't it. I got: b'\\xff\\xff\\xff'`

- After some research, it turns out `\xff\xff\xff` is not just a string. It means 3 bytes of `0xFF(hex)` or `255(dec)`, thus `\xff\xff\xff`. [\xff = one byte of 0xFF(hex)]

- So, it expected the input `hex byte of 0xFF`, which are 3 bytes of `255(dec)`, side-by-side with no space, but it is impossible to type it with keyboard.

- So, I needed to pipe the raw value: 3 bytes of 255 in a way other than typing it directly.  

### 3. Solving Steps

- The code ` sys.stdin.buffer` from `app.py` makes the input a byte object and reads it.

- I used [`printf`](https://www.geeksforgeeks.org/linux-unix/printf-command-in-linux-with-examples/) and piped it into netcat: 
```bash 
printf '\xff\xff\xff\n' | nc <host address> <PORT>
```
This sent the three "0xFF" bytes the program which returned the flag. 

(NOTE: the official hint suggested [pwntools](https://docs.pwntools.com/en/stable/), but the same bytes can be sent with any tool that can produce raw binary output--`printf` )

## Flag

<details>
<summary>Click here to reveal flag</summary>

```text
academy{3ff5_4_d4yz_efbc2747}
```

</details>

## Lessons Learned

- Some byte values (like `0xFF`) are not printable characters and cannot be typed on a normal keyboard. They are outside printable ASCII range. 

- When a program uses ` sys.stdin.buffer` it expects the actual byte values, not the characters.

- a tool like `printf` lets you generate those raw bytes and pipe them over the network. 

- This was my first time dealing with non-printable bytes. Once I understood that the challenge wanted the literal byte `0xFF` three times (not the text `\xff`), the solution became clear.
