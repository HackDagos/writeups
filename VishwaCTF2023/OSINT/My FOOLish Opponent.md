# **Writeup - VishwaCTF**

* Category **OSINT** 
* Name **My FOOLish Opponent** 
* Difficulty **Easy**


## Description
I love to play blindfold chess and this game is one of my easiest win. It's been a long time since I played this game and now I forgot all moves.
Help me recall my game and mention all the moves we played in flag. (btw I was never good in blindfold games what I did was just played against low rated players).


## **Solution**

When I read the description I immediately thought about "Fool's Mate" because the description says that this is a "low-rate game". 

So I tried all the combinations:
VishwaCTF{g4_e5_f4_Qh4#}
VishwaCTF{g4_e5_f3_Qh4#}
VishwaCTF{g4_e5_f4_Qh4#}
VishwaCTF{f3_e6_g4_Qh4#}
VishwaCTF{f3_e5_g4_Qh4#}
VishwaCTF{f4_e6_g4_Qh4#}
VishwaCTF{f4_e5_g4_Qh4#}
...

And I finally got the flag: **VishwaCTF{f3_e6_g4_Qh4#}**

