# L3ak CTF 2025 - OSINT : Sunny Day

* Write-Up Author: [Atlas](https://github.com/Atlas002) - [0xECE](https://www.linkedin.com/company/asso0xece/)
* All credits for the challenge go to [L3ak Team](https://l3ak.team/).

<details>

<summary>Flag</summary>

L3AK{sUn5H1Ne\_iN\_L1ecHt3nSTe1n}

</details>

## Challenge Description:

[360° View of the challenge](https://geosint.ctf.l3ak.team/L3akCTF-sunny_day)

![chall1](<../../../.gitbook/assets/chall1 (3).png>)\
![chall1](<../../../.gitbook/assets/chall2 (3).png>)\
![chall1](<../../../.gitbook/assets/chall3 (2).png>)\
![chall1](<../../../.gitbook/assets/chall4 (2).png>)

## Write up

When first looking around the view we have, we can see a valley in between mountains with healthy vegetation, hinting us toward Europe.

Looking a bit closer we notice a flag waving in the distance :

![flag](<../../../.gitbook/assets/flag (3).png>)

A quick reverse image search reveals that this is **Liechtenstein's flag**

![flag-search](../../../.gitbook/assets/flag-search.png)

We can then assume we are in Liechtenstein.

Next we can spot an unusual structure among the building of the town :

![building](../../../.gitbook/assets/building.png)

Again, reverse image search gives us a hit in **Liechtenstein** which corroborates what we've found so far :

![build-search](../../../.gitbook/assets/build-search.png)

Going on the [result's website](https://aroundus.com/p/5907574-parish-church-triesenberg) we can now see that the building in question is **Triesenberg's parish church**

![build-website](../../../.gitbook/assets/build-website.png)

Now that we know our approximate location, we head over to google maps to find the exact spot :

![map](<../../../.gitbook/assets/map1 (5).png>)

Seeing as the point of view we have is higer up that the church, we head over to the heights of Triesenberg

![map](<../../../.gitbook/assets/map2 (4).png>)

Bingo, we're now at the same point of view as the challenge. Here's the spot of the challenge :

![sat](<../../../.gitbook/assets/sat1 (1).png>)

![sat](<../../../.gitbook/assets/sat2 (1).png>)

Dropping a pin to the right place gives us our flag :

![flag](<../../../.gitbook/assets/result (1).png>)

## Results

`L3AK{sUn5H1Ne_iN_L1ecHt3nSTe1n}`
