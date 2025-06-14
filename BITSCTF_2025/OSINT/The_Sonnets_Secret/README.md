# BITSCTF 2025 - OSINT : The Sonnets Secret 

- Write-Up Author:  [Atlas](https://github.com/Atlas002) - [0xECE - 3](https://www.linkedin.com/company/asso0xece/posts/?feedView=all)

- All credits for the challenge go to [BITSkrieg](https://www.linkedin.com/company/bitskrieg/posts/?feedView=all).
<details>
<summary>Flag</summary>
BITSCTF{Sinclairs}
</details>

## Challenge Description:

In misty glens where thistles grow,  
A tale of treachery, dark and low.  
Where stone walls whisper ancient lore,  
Of crowns that fell to rise no more.  

Seek ye the place where rivers meet,  
Where royal blood once stained the street.  
A castle's shadow looms nearby,  
Its secrets locked in mortar dry.  

Not Elsinore, but kindred shame,  
Where kinsmen plotted, took their aim.  
The crown did fall, a nation reeled,  
In Scotland's heart, the truth concealed.  

Where cobbles echo footsteps past,  
And ghosts of kings their shadows cast,  
The answer lies, if you dare seek,  
In halls where history doth speak.  

Find where the old and new entwine,  
Where modern glass meets ancient spine.  
The murder's stage, now tourist's fare,  
Reveals itself to those who dare.  

Beneath the mist of ages gone,  
A city's heart still beats on,  
Where alleys twist and chimneys smoke,  
And ancient stones their tales invoke.  

Seek ye the place where justice dwells,  
In chambers where the truth compels,  
A door of crimson, walls of white,  
Guard secrets of that fateful night.  

Near where the deed was darkly done,  
A guardian of rights has won,  
His fortress stands, a beacon bright,  
For those who'd challenge crown and might.  

In shadows of the old town's reach,  
Where history and present meet,  
The answers to this riddle lie,  
For those with keen and searching eye.  

Not far from where the monarch fell,  
A modern Portia casts his spell,  
With crimson door and snowy wall,  
He stands where justice casts its pall.  

Defender of the accused and shamed,  
This legal eagle, justly famed,  
Near murder's ground, both old and new,  
Awaits to give the devil his due.  

A gentleman of law, not dame,  
His office near the scene of shame,  
Where ancient wrongs and modern plights,  
Find voice in his impassioned fights.  

His name, a regal echo strong,  
Of kings who ruled when knights were young,  
A Henry bold, with George before,  
Defends where once a crown was wore.  

Now seek the plate upon the door,  
The final clue you're searching for,  
What name is etched in letters clear?  
The answer to our riddle dear.  


## Write up  

[Work in Progress]

[LOCATION => PERSON => FLAG]

*Caveat: I am currently writing this WU several months after the CTF took place. I am trying to reenact the way of thinking I employed as best as possible*

This challenge mainly relies on deduction and reading between the lines. We'll try to look into the relevant bits of the poem:
```
Where royal blood once stained the street.
```
```
Where kinsmen plotted, took their aim.  
The crown did fall, a nation reeled, 
```
=> [Murder of Lord Darnley in Edinburgh, Scotland](https://en.wikipedia.org/wiki/Murder_of_Lord_Darnley)

```
In Scotland's heart, the truth concealed. 
```
=> Capital of Scotland, Edinburgh

```
Find where the old and new entwine,  
Where modern glass meets ancient spine.  
The murder's stage, now tourist's fare,  
```
=> murder took place in the [Old Provost's House of The Collegiate Church of St Mary in the Fields](https://en.wikipedia.org/wiki/Kirk_o%27_Field), which is now the [Old College](https://en.wikipedia.org/wiki/Old_College,_University_of_Edinburgh) which is a [tourist destination](https://www.tripadvisor.co.uk/ShowUserReviews-g186525-d313460-r743084694-University_of_Edinburgh-Edinburgh_Scotland.html), conforts us in our findings.

```
In misty glens where thistles grow,
```
=> thistle, [national flower](https://www.visitscotland.com/things-to-do/attractions/arts-culture/thistle) of scotland 
``` 
Seek ye the place where justice dwells,  
In chambers where the truth compels,
```
=> justice? 

```
A door of crimson, walls of white,  
Guard secrets of that fateful night.  
```
=> red door with white wall close to the secret? 

```
A guardian of rights has won,  
```
=> Someone defending rights, lawyer?


## Results

From our investigation, we can assume the flag to be :

`BITSCTF{Sinclairs}`

Thank you for reading this far, again, huge props to [BITSkrieg](https://www.linkedin.com/company/bitskrieg/posts/?feedView=all) for coming up with this challenge.
