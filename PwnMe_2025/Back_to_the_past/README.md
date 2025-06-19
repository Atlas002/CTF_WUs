# PwnMe 2025 - Reverse : Back to the Past 

- Write-Up Author:  [Atlas](https://github.com/Atlas002) - [0xECE - 3](https://ctftime.org/team/371280)

- All credits for the challenge go to [Phreaks 2600](https://x.com/phreaks2600).
<details>
<summary>Flag</summary>
PWNME{4baf3723f62a15f22e86d57130bc40c3}
</details>

## Challenge Description:
Using the provided binary and the encrypted file, find a way to retrieve the flag contained in flag.enc.

Note : the binary would have been run in May 2024.

Flag format: PWNME{.........................}

[backToThePast](src/backToThePast)  
[flag.enc](src/flag.enc)

## Write up  

### 1. Quick Look Inside the Program

I loaded `backToThePast` into Ghidra  to see what it does:

1. **Seeding a Pseudo-Random Generator**
   I found code that looks like this in C-style pseudocode:

   ```c
   void srand(time_t t) {
     seed = t - 1;
   }
   uint32_t rand() {
     seed = seed * 0x5851F42D4C957F2D + 1;
     return seed >> 33;
   }
   ```

   * **`srand(time)`** sets an internal number called `seed` to “current time minus 1.”
   * **`rand()`** then turns `seed` into a new number each time you call it. We’ll use those numbers to “encrypt” or “decrypt.”

2. **The Encryption Loop**
   Later, I saw a loop that for each byte:

   * Reads one byte from the input.
   * Calls `rand()` to get a number.
   * Does a few twists and shifts on that number.
   * XORs (bitwise-XOR) the file byte with the low 8 bits of that twisted number.
   * Writes the result out.

   XOR is its own inverse, so if we repeat the same steps on the encrypted file, we’ll get the original back—**provided** we use exactly the same sequence of “random” numbers and twists.

---

### 2. Reproducing the “Twists and Shifts”

The “few twists and shifts” were about 10 assembly instructions (multiplying by a big constant, shifting right, adding, shifting again, subtracting, etc.). It looked complicated at first, but the idea is straightforward:

1. **Start** with the 32-bit output from `rand()`.
2. **Sign-extend** it (treat it as a signed number).
3. **Multiply** by a constant (`0xffffffff81020409`).
4. **Shift right** 32 bits.
5. **Add** the original 32-bit value.
6. **Shift right** 6 bits (arithmetic shift: keeps the sign).
7. **Extract** the sign bit of the original and subtract it.
8. **Shift left** 7 bits, subtract again.
9. **Subtract** from the original value one more time.

All of these steps produce a final 32-bit result. We take **just the lowest 8 bits** of that result as our XOR mask for one byte.

I translated those steps **line by line** into a small Python function. You can test it prints different masks each call to make sure it’s varying.

---

### 3. Brute-Forcing the Time

Because we know the program used “current time in May 2024” as its seed, we can simply try every possible second in May:

* May has 31 days → 31 × 24 × 3,600 = 2,678,400 seconds.
* For each candidate timestamp `t`:

  1. Set `seed = t - 1`.
  2. For each byte of `flag.enc`, call our Python version of `rand()` and do the same twists, then XOR the encrypted byte.
  3. After processing all bytes, check if the result starts with `PWNME{`.
  4. If it does, we’ve found the right time – we can stop.

Even in pure Python, processing \~2.7 million seeds × 39 bytes finishes in seconds on a modern machine.

---

### 4. The Simple Python Script

Here’s the minimal Python code I ended up running. You don’t need to understand every line—just see how it maps the above steps:

```python
import struct, time

# Read the encrypted file
enc = open("flag.enc", "rb").read()

# Try every second in May 2024
start = int(time.mktime(time.strptime("2024-05-01", "%Y-%m-%d")))
end   = int(time.mktime(time.strptime("2024-06-01", "%Y-%m-%d")))

for t in range(start, end):
    seed = (t - 1) & 0xFFFFFFFFFFFFFFFF
    out = bytearray(enc)

    # Decrypt each byte
    for i in range(len(out)):
        # musl-rand: update seed and extract 32 bits
        seed = (seed * 0x5851F42D4C957F2D + 1) & 0xFFFFFFFFFFFFFFFF
        r = (seed >> 33) & 0xFFFFFFFF

        # The “twists and shifts” from the binary
        magic = 0xffffffff81020409
        if magic & (1 << 63):
            magic -= (1 << 64)
        edx = (struct.unpack("q", struct.pack("Q", r))[0] * magic) >> 32
        edx = (edx + r) & 0xFFFFFFFF
        edx_s = struct.unpack("i", struct.pack("I", edx))[0] >> 6
        ecx_s = struct.unpack("i", struct.pack("I", r))[0] >> 31
        diff = edx_s - ecx_s
        ecx2 = ((diff << 7) & 0xFFFFFFFF) - diff
        eax_s = struct.unpack("i", struct.pack("I", r))[0] - ecx2
        xor_mask = eax_s & 0xFF

        out[i] ^= xor_mask

    # Check for the magic prefix
    if out.startswith(b"PWNME{"):
        print("Flag:", out.decode())
        break
```

1. **Read** the encrypted file into `enc`.
2. **Loop** over every second in May.
3. **Seed** our custom PRNG (`seed = t - 1`).
4. **Decrypt**: for each byte, update the seed, calculate the mask, XOR.
5. **Check** if the result looks like a flag.

When I ran this, I got:

```
Flag: PWNME{4baf3723f62a15f22e86d57130bc40c3}
```


## Results

Therefore, our flag is :

`PWNME{4baf3723f62a15f22e86d57130bc40c3}`

Thank you for reading this far, again, huge props to [Phreaks 2600](https://x.com/phreaks2600) for coming up with this challenge.
