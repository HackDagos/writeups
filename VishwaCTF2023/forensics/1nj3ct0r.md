# **Writeup - VishwaCTF**

* Category **Forensics** 
* Name **1nj3ct0r** 
* Difficulty **Hard**


## Description

You Are Working As Digital Forensics Expert At Infosys India And Someone Reported That A PC Might Have Been Infected. Tech Team Already Collected All The Evidences From Workstation And Found That Someone Injected Malicious Code. It Is Your Job To Find, what Is Injected Into That PC.

NOTE:Use Underscore(_) After Every Word.


## **Solution**

The challenge give you a file "usbforensics.pcapng", you can open it with **Wireshark**, there are 278 packets with the USB / USBHUB protocols.

Use this filter: usb.data_flag && usb.data_len == 2 and export the data.

flag: **VishwaCTF{n0w_y0u_423_d0n3_w17h_u58_f023n51c5}**
