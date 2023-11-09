# Petshop Pro

### Website: [CTF-Hacker101](https://ctf.hacker101.com/ctf)
Date: 11/08/2023

-----------------------------------------------------------------
Task: Hunt down all the flags, example of flag given by CTF-Hacker101. There are total of 3 flags to be found.

[How to Play](https://ctf.hacker101.com/howtoplay)

```css
$$^FLAG^37ae568362f974017fa575f08cd215044cd6bb395c3f5e5e293ee5324ba6769c$FLAG$
```
![](/CTF-Hacker101/Easy/Images/Petshop-image1.png)

## Let's Begin

### Tools Needed:
[Wordlist for Username and Password](https://github.com/jeanphorn/wordlist/tree/master)<br>
[SecList Username and Password](https://github.com/danielmiessler/SecLists/tree/master)<br>
[RockyouList](https://github.com/brannondorsey/naive-hashcat/releases/download/data/rockyou.txt)<br><br>

<b>Option 1:</b>
Burp Suite Community Edition (or Pro)
Turbo Intruder tool for Burp Suite<br>
<b>Option 2:</b>
Kali Linux/Parrot OS
Hydra

### Steps
![](/CTF-Hacker101/Easy/Images/Petshop-image2.png)
1. We start entering this CTF by exploring what the website has to offer. Of course we will inspect the page, while exploring what it has.
   Nothing looks out of the ordinary or so we think. So lets go add something to the cart and check out.
   
![](/CTF-Hacker101/Easy/Images/Petshop-image3.png)

2. Well this is interesting the checkout see to be broken maybe? So lets go ahead and inspect the code and see what it shows.
   Go ahead and head back to the previous page, the checkout page. When you open the page you should be able to see the input tag showing type = "hidden".
3. Now why would this be hidden, well we don't care about it being hidden, we care about the value. After playing around with the value. We can see that if
   set the price of either pet (or as many you have added to the cart, preferably one pet should do the trick) to zero, then check out. We see that the flag
   is generated.
   
![](/CTF-Hacker101/Easy/Images/Petshop-image4.png)   
<Code>Flag 1/3</Code>

4. Now at this point, you may not know what else to do. You can use different tools to see what else there is more to about the webpage.
   The hint can also tell you what is the next step. I played around and took a look at the hints (though I know you can use Fuff in Linux). 
   However I use the hints to help me, and learn that the is a login page. So by adding */login* at the end of the url, I am taking to the admin login page. 

![](/CTF-Hacker101/Easy/Images/Petshop-image5.png) 

5. You probably try all the default possible credential that you can think of to get into page. However it won't work. Well we need to brute force this.
   Trust me when I say this. This was the most painful and time consuming brute force I've done, I had to research, download, play around with many tools, and 
   it lead me back to Burp Suite.
   **Note**: I have no experience in Hydra or Burp Suite until this CTF. After three days of attempting to find the best efficient way to brute force, 
    I gain a small experience in using the application.

   For those who use hydra, you can do it via the proxy way or url way. Below is just copying the url. In case you lose connection or accident force quit
  <code>sudo hydra -R</code> to resume the session.
```html
sudo hydra -L /usr/share/wordlist/rockyou.txt -p admin -t 40 [replace this with your url without https://] https-post0form "/login:username=^USER^&password=^PASS^:Invalid username"
```
*Replace Invalid Username with Invalid Password when you find the username (replace ^USER^ with the username you found.*

6. For those using Burp Suite, good news. I suffer so you won't have to. The free edition of this application is awful for Brute Forcing, free version throttle. To avoid that we will want to install the Turbo Intruder version, which will save us some time and sanity.

7. Download Burp Suite, then launch it. Go to Extension Tab > BApp Store > Search for Turbo Intruder and intall it. (I am using v2023.10.2.5 at the time of this writing, it may change future version).

8. Click on Proxy tab > Open Browser > Copy and Paste the URL into the Burp Browser. Type whatever in the username and password (I just use admin admin). 
   Turn on Intercept, then you be presented with the Raw of the URL. Highlight the word admin where the username is. Right Click on it > Extension > Turbo   Intruder > Send to Turbo Intruder.

9. You be taking to the Turbo Intruder Page. Here is the website to figure out how to brute force: [Turbo Intruder for Burp](https://exploit-notes.hdks.org/exploit/web/tool/turbo-intruder-in-burp-suite/)
   Good news, I done the work for you. I use Windows 11 Pro for this, you may have to change your file path. At the time I use rockyou.txt, username.txt, and 
   names.txt to help me crack it. I ran all three and took roughly 15-20 minutes to get me the username then that password. So total 30 to 40 minutes roughly.
   Replace 'Invalid username' with 'Invalid password' once you find the username. Make sure to replace the admin with the username. Go ahead and click Attack button near the bottom and play the waiting game.

```c++
def queueRequests(target, wordlists):
    engine = RequestEngine(endpoint=target.endpoint,
                           concurrentConnections=5,
                           requestsPerConnection=100,
                           pipeline=False
                           )

    for word in open('C:/Users/{USER}/Desktop/rockyou.txt'):
        engine.queue(target.req, word.rstrip())

def handleResponse(req, interesting):
    if 'Invalid username' not in req.response:
        table.add(req)
```
10. Once you are in your are present with the flag. Go ahead and submit it.

![](/CTF-Hacker101/Easy/Images/Petshop-image6.png) 

<Code>Flag 2/3</Code>

11. We are almost done. The next part is a bit tricky. Go ahead and click on 'Edit', does not matter which you pick.
12. Here base on the previous CTF, this is likely an injection method. We can do either alert given below. Then test all of the input box.
    Of course, one of them will give us an error, so play around and remove the likely one that produce the error, it is mostly likely the price input.
    If you chosen the script alert, after saving and heading back to the previous page, it should give you a Flag on the alert.
    The image source should give you the flag after you save the input, then add said item to the cart. The flag will appear in the checkout page.
    
```html
<script>alert(document.domain)</script>
<img src=x onerror=alert(1)>
```
<Code>Flag 3/3</Code>

### Conclusion
This challenge was tedious and lots of waiting. If you have not use hydra or Burp Suite, I suggest doing some search to learn it. Same with Fuff for Linux. These may help you in future challenges. Trying different option and going in circle, I learn a lot about how to solve and learn a bit of said applications. Be expose to these certain things helps me learn something new everyday.

