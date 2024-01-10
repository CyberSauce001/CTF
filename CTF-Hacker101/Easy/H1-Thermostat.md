# H1 Thermostat

### Website: [CTF-Hacker101](https://ctf.hacker101.com/ctf)
Date: 01/09/2024

-----------------------------------------------------------------
Task: Hunt down all the flags, example of flag given by CTF-Hacker101. There are total of 4 flags to be found.

[How to Play](https://ctf.hacker101.com/howtoplay)

```css
$$^FLAG^37ae568362f974017fa575f08cd215044cd6bb395c3f5e5e293ee5324ba6769c$FLAG$
```
![](/CTF-Hacker101/Easy/Images/H1-Thermostat-Image1.png)

## Let's Begin

### Steps
Step 1) We begin by starting the CTF and waiting for the web browser to let you know to refresh. Once it pops up the message to refresh. 
Go ahead and refresh your browser. 

Step 2) A Android APK link should pop up, go ahead and download it. You can go ahead and download an emulator to see how the APK works, 
but it is not necessary to solve it. 

Step 3) In order to reverse-engineer the APK file, you need to download the following APK decompiler tool: 
  - JADX
  - Apktool
  - Bytecode Viewer
  - Visual Code Studio -> I believe you need some type of extension install to view it.

Step 4) After downloading the following decompliler, open the APK file. Once you open the file. Go ahead and explorer the APK. You will come and one of the drop-down menu label 'hacker101.level11'. This is the main interest to find our flag.

Step 5) Exploring each menu under 'hacker101.level11', we come across the menu 'PayloadRequest'
Opening it up we can see both flags giving. One in messageDigest.update and the other in this.mHeaders.put.

Step 6) Copy and paste both flags and you are done.

![](/CTF-Hacker101/Easy/Images/H1-Thermostat-Image2.0.png)

<Code>Flag 2/2</Code>

### Conclusion
Although I am not a fan of reverse-engineering apk files, I find this to be simple and easy to get into reverse-engineering. Although you have to do a bit of research and find the best decompliler tool that will work for you.

