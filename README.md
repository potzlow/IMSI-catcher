# IMSI-catcher-de
Dieses Programm zeigt dir die IMSI Nummern von Mobiltelefonen in deiner Umgebung an.

This program shows you IMSI numbers of cellphones around you.  

/!\ Das Programm wurde zu wissenschaftlichen Zwecken entwickelt, um z.B. GSM besser zu verstehen. Halte dich an die HackerEthik!
  
/!\ This program was made to understand how GSM network work. Not for bad hacking !  
  

![screenshot0](capture_simple_IMSI-catcher.png)  
  

Was du brauchst
=============
1 PC mit mehr als 3 GB RAM * zum kompilieren von gr-gsm  
1 USB DVB-T Stick (RTL2832U) mit Antenne (unter 15€)  
  
\* *On EEEPC 1000H with 2Go of RAM and 2Go of swap, compiling take 1 day.*  
  
Setup
=====

```
cd /tmp
sudo apt-get install gnuradio git python-scapy
git clone https://github.com/pybombs/pybombs.git
cd pybombs
```
/!\ Wenn "./pybombs config" dich nach dem "prefix" fragt, setze "/usr/local" :  
prefix [/tmp/target]:/usr/local  
```
./pybombs config
```
```
sudo ./pybombs install gr-gsm
echo "[grc]
local_blocks_path=/usr/local/share/gnuradio/grc/blocks
" > ~/.gnuradio/config.conf
```

Run
===
  
In terminal 1  
```
sudo python simple_IMSI-catcher.py
```

In terminal 2  
```
airprobe_rtlsdr.py
```
Now, change the frequency and stop it when you have output like :  
```
15 06 21 00 01 f0 2b 2b 2b 2b 2b 2b 2b 2b 2b 2b 2b 2b 2b 2b 2b 2b 2b
25 06 21 00 05 f4 f8 68 03 26 23 2b 2b 2b 2b 2b 2b 2b 2b 2b 2b 2b 2b
49 06 1b 95 cc 02 f8 02 01 9c c8 03 1e 57 a5 01 79 00 00 1c 13 2b 2b
...
```
Now, watch terminal 1 and wait. IMSI numbers should appear :-)  
If nothing appears after 1 min, change the frequency.  
  
Doc : https://fr.wikipedia.org/wiki/Global_System_for_Mobile_Communications  
Example of frequency : 9.288e+08 Bouygues  
  
You can watch GSM packet with  
```
sudo wireshark -k -Y '!icmp && gsmtap' -i lo
```
  
Links
=====

Setup of Gr-Gsm : http://blog.nikseetharaman.com/gsm-network-characterization-using-software-defined-radio/  
Frequency : https://fr.wikipedia.org/wiki/Global_System_for_Mobile_Communications  
Mobile Network Code : https://fr.wikipedia.org/wiki/Mobile_Network_Code  
Scapy : http://secdev.org/projects/scapy/doc/usage.html  
IMSI : https://fr.wikipedia.org/wiki/IMSI  
Realtek RTL2832U : http://doc.ubuntu-fr.org/rtl2832u and http://doc.ubuntu-fr.org/rtl-sdr  
