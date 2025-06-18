# AMSI CTF 2025 - OSINT : Échauffement

- Write-Up Author:  [Atlas](https://github.com/Atlas002) - [0xECE - CyberSharks](https://ctftime.org/team/389816)

- All credits for the challenge go to [AMSI](https://www.linkedin.com/company/association-du-master-s%C3%A9curit%C3%A9-informatique/)

<details>
<summary>Flag</summary>
AMSI{arbuste.clouter.ouvrir}
</details>

## Challenge Description:

Un petit échauffement est toujours nécessaire avant un gros effort.

Utilisez what3words pour renvoyer les coordonées.

Format du flag : AMSI{radiographique.jade.bitumons}

![image](img/chall.jpg)

## Write up  

My first reflex with any image is to look at metadata, but no luck here on this one.

Looking at the image, the first thing that jumps to the eyes are these two vertical buildings that look like lighthouses :

![belv1](img/belv.png)

With a quick google search we end up finding that these are the [belvédères of Deauville](https://g.co/kgs/VRbXdhp) 

![search1](img/imgSearch1.png)

Looking further into it we learn that they are located near [Deauville's harbor](https://www.google.com/url?sa=t&source=web&rct=j&opi=89978449&url=/maps/place//data%3D!4m2!3m1!1s0x47e1d51e068b0a6f:0x1f968b5cba2460c0%3Fsa%3DX%26ved%3D1t:8290%26ictx%3D111&ved=2ahUKEwil66iZ7vqNAxXRWqQEHSVDNpYQ4kB6BAg3EAM&usg=AOvVaw0AO6V4JQHpdKjAK4JPSbgr)

![img](img/map1.png)

Since they aren't very tall buildings, we can assume that the picture was taken not too far from there.


Looking a bit more at the picture, we notice a second interesting element : 

![church]()

This looks like a chruch undergoing some restoration work.

Looking up `Church restoration Deauville`



## Results

`AMSI{arbuste.clouter.ouvrir}`