# TJCTF2025 - Forensic : Deep Layers 

- Write-Up Author:  [Atlas](https://github.com/Atlas002) 

- All credits for the challenge go to [TJCTF Team](https://www.tjcsec.club/)

<details>
<summary>Flag</summary>
tjctf{p0lygl0t_r3bb1t_h0l3}
</details>

## Challenge Description:

Not everything ends where it seems to...

[Challenge file]()

## Write up  

Using `zsteg` and `strings` on the .png file gives us this : 

![scan1]()

We can see that a `secret.gz` zipped folder is hiding in the file, and also the meta password string : `(base64)`

We then extract the hidden file by skipping the "irrelevant" bits : 

![extract1]()

We then get the file `hidden.zip` that requires the meta password we got decoded from base64 : `p0lygl0otp3ssw0rd`

![extract+decode]()

We then get the `secret.gz` taht we unzip with `gunzip` :

![extract]()

We then obtain the `secret` file which we `cat` to get the flag :

![catflag]()

we then
## Results

`tjctf{p0lygl0t_r3bb1t_h0l3}`
