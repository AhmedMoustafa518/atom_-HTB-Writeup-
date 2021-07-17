# atom_-HTB-Writeup
This  is my first Writeup

Machine      : Atom



Difficulty   : MEDIUM


![1](https://user-images.githubusercontent.com/64806211/126027857-1291cb8f-f41d-4fde-afa4-f621ab74b2fe.png)


1- First make sure you're connected to the machine 

![2](https://user-images.githubusercontent.com/64806211/126027941-56145f26-0e5e-465d-9519-bfdac3a3963c.png)

2- second step have to do is making a scan with nmap


>`nmap -sC -sV -Pn 10.10.10.237`



![22](https://user-images.githubusercontent.com/64806211/126028146-0b149bb6-ffe5-4b84-8a8f-745ebad2446e.png)

![3](https://user-images.githubusercontent.com/64806211/126028026-f28b60f4-1e1c-4782-a5bd-1570af7863b3.png)

So here we got 4 open ports


GREEEEEEEEEEET"""


After checking the site, I couldn't find anything 


!So let's try smbclient 




> `smbclient --list //10.10.10.237/ -u`


![4](https://user-images.githubusercontent.com/64806211/126028702-2f69539a-4280-4db8-a59c-9931abe42764.png)


I found file called Software_Updates 


let's check it out 


>`smbclient -N //10.10.10.237/Software_Updates -u`


















>`ls`




>`get UAT_Testing_Procedures.pdf`

After viewing the pdf 


I found interesting part  :


![6](https://user-images.githubusercontent.com/64806211/126030973-c291e4e2-9267-4e63-814a-6ceca3d19e10.png)


So that means  we could just modify  one of the 3 
client files we found before the server will run the files and execute what’s the inside …. 



I searched alot on google to find somthing interesting about `electron-builder`
and i found alot of blogs and wepsites talking about that and what is used for



So i make a fake `latest.yml`to bypass the payload security check and excute it directly
so i write the shell what will excute our payload to allow us gegt a REV- 
so you can `dowmload` it using terminal :
