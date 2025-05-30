# BITSCTF 2025 - OSINT : Hot Pause 

- Write-Up Author:  [Atlas](https://github.com/Atlas002) - [0xECE - 3](https://www.linkedin.com/company/asso0xece/posts/?feedView=all)

- All credits for the challenge go to [BITSkrieg](https://www.linkedin.com/company/bitskrieg/posts/?feedView=all).
<details>
<summary>Flag</summary>
BITSCTF{that_was_a_very_weird_OSINT_challenge_afd12df}
</details>

## Challenge Description:

What even is OSINT about this?

nc {challenge.IP} 8000

[Concert.mp4](/BITSCTF_2025/OSINT/Hot_pause/vid/concert.mp4) 

## Write up  

### Part 1/3

When we first connect to the given IP address, we're greeted by this message : 

```
Welcome secret agent. 
We've recovered a video from our aliases infiltrating our next target. 
Your first task is to find out what is our target city. 

City Name (all caps): 
```

We then go to our video file and the more astute will quickly recognise a concert of the band Coldplay performing the song "Yellow". 

By taking a snapshot of the video where the stage is visible and doing an image search on Google, we end up on this Instagram post :

![igpost](/BITSCTF_2025/OSINT/Hot_pause/img/image1.png)

The stage is very similar, we see that it's the same band playing the same song, and it lists 'Ahmedabad 2025' along with it. 

By digging into this, we learn that coldplay indeed played in the [Narendra Modi Stadium](https://www.coldplay.com/tour-date/narendra-modi-stadium-2/), located in `Ahmedabad`.

Entering this in the console will lead us to the next step. 

### Part 2/3

```
City Name (all caps):AHMEDABAD
Correct!

Well done! Now you need to find out where our partner agent was sitting. 

Block Letter with Bay(For eg. A5,B1 etc.): 
```

For this question we look up  `Coldplay Ahmedabad Concert Seating Plan` and find this :

![seatmap](/BITSCTF_2025/OSINT/Hot_pause/img/image2.png)

From the video we can see that the person filming is located on the right side of the stage, and when he pans over the stadium we can see that he's pretty far forward.  
With some deduction *(and a pinch of luck)*, we can find that our guy is sitting in section `Q3`.

Once again, entering this in the console will lead us to the next and final step.

### Part 3/3

```
Block Letter with Bay(For eg. A5,B1 etc.): Q3
Correct!

Good work. Now when you hear Chris Martin say "You know I love you so...." 
for the beat drop, I need you to use your Flipper Zero to send the correct 
data stream, replicating the wristbands colour exactly. Our enemies should 
have no clue. Good Luck. 

Data Stream: 
```

Some hardware in OSINT, why not!

By looking up `Coldplay concert wristband`, we end up on a link titled [Pixmob | Coldplay – Music of the Spheres World Tour](https://pixmob.com/projects/coldplay). Digging deeper into this we learn that Coldplay is using Pixmob Wristbands for their show.

We then Google `pixmob color code datastream`, where we find [this](https://github.com/danielweidman/flipper-pixmob-ir-codes/blob/main/pixmob_all_colors.ir) repo, listing all colors achievable with a pixmob wristband and their respective datastream. 

Looking at the video, we see that at the specified moment the wristbands turn a bright yellow, which corresponds to the datastream : `1400 1400 700 700 700 700 1400 2800 700 2100 700 700 700 1400 700 1400 1400 2800 1400 2800 700`.

Entering this into the console will give us the challenge's flag : 

```
Data Stream: 1400 1400 700 700 700 700 1400 2800 700 2100 700 700 700 1400 700 1400 1400 2800 1400 2800 700

Correct!

Good Job agent. Here's your flag, should you choose to accept it: 
BITSCTF{that_was_a_very_weird_OSINT_challenge_afd12df}
```


## Results

Based on the console answer, the flag is :

`BITSCTF{that_was_a_very_weird_OSINT_challenge_afd12df}`

Thank you for reading this far, again, huge props to [BITSkrieg](https://www.linkedin.com/company/bitskrieg/posts/?feedView=all) for coming up with this challenge.
