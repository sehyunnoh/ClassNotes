## assignment 
```linux
sudo tail -n5 /etc/passwd 
sudo userdel -rf tim

sudo groupdel techs 
sudo tail -n5 /etc/group  

2.

sudo addgroup cartoons
sudo addgroup simpsons
sudo addgroup familyguy
sudo addgroup futurama

sudo useradd -m -c "Homer Simpson - Nuclear Operator" -p `mkpasswd 23451` -G simpsons,cartoons -s /bin/bash  simpsonh


sudo passwd -e simpsonh
sudo passwd -e simpsonb
sudo passwd -e flandersn
sudo passwd -e griffinp
sudo passwd -e quagmireg
sudo passwd -e griffins
sudo passwd -e bendingb
sudo passwd -e fryp
sudo passwd -e leelat

su bendingb

sudo usermod -e 2019-10-17 bendingb
sudo chage -l bendingb 


3. root 권한으로 변경
   umask 0007
   mkdir -p Cartoons/{FamilyGuy,Futurama,SharedFiles/{docs,music,videos},Simpsons}
   
   chown :cartoons ./Cartoons/
   chown :familyguy ./FamilyGuy/
   chown :futurama ./Futurama/
   chown :cartoons ./SharedFiles/
   chown :cartoons ./docs/
   chown :cartoons ./music/
   chown :cartoons ./videos/
   chown :simpsons ./Simpsons    

   chmod g+S ./SharedFiles/
   sharedfile 폴더로 이동
   touch birthdays.txt 
	

	- 리눅스 과제 
	  -> history 캡쳐 부분만
	  -> show는 한 유저만 보이면 됨.
	     sudo userdel -rf bhomer
		 tail -n3 /etc/passwd
		 cat /etc/group
		 sudo groupdel techs
		 tail -n3 /etc/group
		 sudo change -l simpsong
		 sudo date -s 2014-10-20
		 su - bendingb
		   -> your account has expired.
		 su - simpsonh
		 
		 
- 질문
  -> root로 변경 하려면 비번은? (매번 sudo 붙이기 힘듦)		
  -> sudo su  
```