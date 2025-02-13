# Prologue
Git is a tooling to support developer in various way. For example : code control version , ability to co-ordinate code with team

## Preparation
1. Register [Github](https://github.com/)
2. Install [Git](https://github.com/git-guides/install-git)
3. Install [VS Code](https://code.visualstudio.com/download) with extension below  
    - Git Graph
    - GitHub Pull Requests and Issues
    - GitHub Repositories

## SSH key
SSH Key เป็นกุญแจสำหรับเข้าใช้ระบบโดยไม่ต้องใช้รหัสผ่าน มีการสื่อสารแบบเข้ารหัส นิยมใช้กับ ssh บน Linux จะเก็บ Private Key ไว้ในเครื่อง Desktop/Laptop ที่เราใช้งานอยู่(Local) ส่วนเซิร์ฟเวอร์ (Remote) ที่จะเข้าใช้เก็บ Public Key
ซึ่งสามารถศึกษาเรื่องการเข้ารหัสเพิ่มเติมได้ทางนี้ [4 Cryptography Concept](https://medium.com/scb-techx/4-cryptography-concept-%E0%B8%97%E0%B8%B5%E0%B9%88-developer-%E0%B8%97%E0%B8%B8%E0%B8%81%E0%B8%84%E0%B8%99%E0%B8%84%E0%B8%A7%E0%B8%A3%E0%B8%A3%E0%B8%B9%E0%B9%89-15a806b6771d)

### การสร้าง SSH key
- เปิด window terminal
- สร้าง SSH key ด้วยคำสั่ง(แก้อีเมลล์ให้เหมาะสม) 
>ssh-keygen -t ed25519 -C "your_email@example.com"
- ใส่ชื่อไฟล์ในตัวอย่างตั้งชื่อ id_github ถ้ายังไม่เคยสร้างมาก่อน แนะนำให้ตามค่า default ไปก่อนเพราะจะสร้างโฟลเดอร์ .ssh ให้ด้วย
- Enter passphrase ให้เคาะผ่านไม่ต้องป้อน แล้วเคาะผ่านอีกรอบ
- ตัวอย่างด้านล่างทำบนวินโดว์ ส่วน macOS และ Linux ก็ทำคล้ายกัน

``` 
PS C:\Users\thiti\.ssh> ssh-keygen -t ed25519 -C "Thitiwut.ekwisit@gmail.com"
Generating public/private ed25519 key pair.
Enter file in which to save the key (C:\Users\thiti/.ssh/id_ed25519): C:\Users\thiti/.ssh/id_github
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in C:\Users\thiti/.ssh/id_github
Your public key has been saved in C:\Users\thiti/.ssh/id_github.pub
The key fingerprint is:
SHA256:DyjD07otLKAXNz2aYcTaLdTTFRVWZGr4M/0Pj+gJo+0 Thitiwut.ekwisit@gmail.com
The key's randomart image is:
+--[ED25519 256]--+
|          .o+++  |
|          .o o   |
|   . . . .. o    |
|   .+.o..  o .   |
|   ==oo.S   + .  |
|. o B=+  o   o . |
|.. =.* .  +   . .|
|. o =o   o o o +.|
| . .... ..E.+ . o|
+----[SHA256]-----+
``` 
- ย้ายไฟล์ id_github.pub และ id_github ซึ่งเป็นpublic/private key ไปเก็บไว้ใน folder .ssh (แนะนำว่าครั้งแรกทำตาม default จะนำไปใส่โฟลเดอร์ .ssh ให้เลย และกำหนดสิทธิ์ที่เหมาะสมให้ด้วย) ไฟล์จะอยู่โฟลเดอร์ .ssh ใต้โฮมโฟลเดอร์ สมมุติผมใช้ login ชื่อ thiti ไฟล์จะอยู่ที่ "C:\Users\thiti\.ssh\id_github" สำหรับ
Linux และ macOS จะอยู่ที่ "~/.ssh/"
- ในโฟลเดอร์ .ssh เปิดหรือสร้างไฟล์ชื่อ config (ถ้ายังไม่มีให้สร้างใหม่ แนะนำให้ใช้ VS Code ในการสร้าง) แล้วใส่ 4 บรรทัดนี้ลงไป
``` 
Host github.com
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_github
``` 
ต้องมีการตั้งค่า parameter username และ email ของ git ในเครื่องตาม github account โดยใช้คำสั่งต่อไปนี้
- command สำหรับ config username
> git config --global user.name "Oatake"
- command สำหรับ config : E-mail
> git config --global user.email "Thitiwut.ekwisit@gmail.com"
- command สำหรับตรวจสอบ config git
> git config --list

หมายเหตุ : สามารถตรวจสอบการเชื่อมต่อ github ได้โดย command ด้านล่าง
>ssh -T git@github.com
จากตัวอย่างด้านล่าง ถ้าหากเป็นการเชื่อมต่อครับแรก จะมีการถามหา fingerprint ให้ทำการว่า "yes" ถ้าหากสำเร็จจะพบข้อความ "Hi Oatake! you've successfully authenticated"
``` 
PS C:\Users\thiti\.ssh> ssh -T git@github.com
The authenticity of host 'github.com (20.205.243.166)' can't be established.
ED25519 key fingerprint is SHA256:+DiY3wvvV6TuJJhbpZisF/zLDA0zPMSvHdkr4UvCOqU.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added 'github.com' (ED25519) to the list of known hosts.
Hi Oatake! You've successfully authenticated, but GitHub does not provide shell access.
``` 
### Credit : schooltechx

VSCode-Extension
vscode-icon 
Tailwind CSS IntelliSense
Prettier - Code formatter
Jest Snippet
Jest
JavaScript (ES6) code snippet
ES7 + React/Redux/React-Native snippets
Auto Rename Tag