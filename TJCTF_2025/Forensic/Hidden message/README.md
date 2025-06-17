# TJCTF2025 - Forensic : Hidden Message

- Write-Up Author:  [Atlas](https://github.com/Atlas002) 

- All credits for the challenge go to [TJCTF Team](https://www.tjcsec.club/)

<details>
<summary>Flag</summary>
tjctf{steganography_is_fun}
</details>

## Challenge Description:

I found this suspicious image file on my computer. Can you help me figure out what's hidden inside?

[challenge file]()

## Write up  

Using `zsteg` on the file reveals the flag hidden in the LSB section  : 

![image]()

## Results



`tjctf{steganography_is_fun}`
