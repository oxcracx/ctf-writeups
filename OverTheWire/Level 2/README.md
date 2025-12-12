## Bandit Level 1 → Level 2
Level 2 Solution

To start solving the level, you need to log in to OverTheWire using SSH: 
"ssh bandit1@bandit.labs.overthewire.org -p 2220", password for this login session is provided on the website, which is “ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If”.

The objective of this challenge is to find a file named “-” in the home directory, which contains the password for the next level.

### Challenge
When I tried to view the contents of the file using cat -, my terminal cursor started blinking, but nothing appeared. 

<img width="806" height="497" alt="Screenshot from 2025-12-12 10-44-49" src="https://github.com/user-attachments/assets/5b9f3227-12d1-4983-8d45-809be6f31675" />


At first, I thought it was a server delay, so I reconnected, but the issue remained the same. After spending more than 30 minutes trying to figure it out, 
I searched on Google and found out that "-" in Linux is a special character. o when I used "cat -", I was basically telling Linux to read input from the keyboard, not from a file. 
That’s why the terminal was blinking and waiting, it was expecting me to type something.

<img width="806" height="538" alt="image" src="https://github.com/user-attachments/assets/ccc69f95-1548-4463-b830-4666ea533192" />


Then I specified the path and made thing simpler for terminal by telling terminal "cat ./-" read file "-" from current directoy.

Commands used:
- ls = lists files and folders in the current directory.
- cat readme = cat is mainly used to view the content of the text file.
- cat ./- = Telling terminal to read file "-" from current directoy "./".




### Password 
263JGJPfgU6LtdEvgfWU1XP5yac29mFx


<img width="806" height="497" alt="image" src="https://github.com/user-attachments/assets/562308ec-8394-40a9-8d74-d47d78f3b9a7" />
