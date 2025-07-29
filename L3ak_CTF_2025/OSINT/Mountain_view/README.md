# L3ak CTF 2025 - OSINT : Mountain View

- Write-Up Author:  [Atlas](https://github.com/Atlas002) - [0xECE](https://www.linkedin.com/company/asso0xece/)

- All credits for the challenge go to [L3ak Team](https://l3ak.team/).

<details>
<summary>Flag</summary>
L3AK{y0sh1n0_HAs_gR3At_54KuRA_Bl0s5omS}
</details>

## Challenge Description:

[360° View of the challenge](https://geosint.ctf.l3ak.team/L3akCTF-mountain_view)

![chall1](img/chall1.png)  
![chall1](img/chall2.png)  
![chall1](img/chall3.png)  
![chall1](img/chall4.png)  
 
## Write up  

When first looking around, we can see that we're pretty high up on a slope, with mountainous backgrounds and some city in the distance. Paired with some sakura trees we can spot nearby, this is strongly hinting us toward **Japan**.

Then, looking a bit closer we can see a sign with kanji written over it : 

![gate](img/gate.png)

A reverse image search give us a direct hit on it :

![gate search](img/gate-search.png)  

![gate result](img/gate-result.png)  

We now know that we are at **Mount Yoshino, Nara Japan**.

Looking up the place on google maps puts us near the starting point : 

![map1](img/map1.png)

Looking back at the view we've been given, we can see that the sign is below our point of view, that there is a sharp turn to the left behind us and a long stretch of road ahead of us.

Putting these informations together leads us to this spot :

![map2](img/map2.png)

Looking around in street view confirms that this is the right place : 

![sview](img/sview.png)

Now the exact spot of the challenge :

![sat](img/sat1.png)

![sat](img/sat2.png)

We then drop our pin and get the flag :

![result](img/result.png)

## Results

`L3AK{y0sh1n0_HAs_gR3At_54KuRA_Bl0s5omS}`

 