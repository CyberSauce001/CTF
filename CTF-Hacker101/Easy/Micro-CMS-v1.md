# Micro-CMS v1

### Website: [CTF-Hacker101](https://ctf.hacker101.com/ctf)
Date: 10/23/2023

-----------------------------------------------------------------
Task: Hunt down all the flags, example of flag given by CTF-Hacker101. There are total of 4 flags to be found.

[How to Play](https://ctf.hacker101.com/howtoplay)

```css
$$^FLAG^37ae568362f974017fa575f08cd215044cd6bb395c3f5e5e293ee5324ba6769c$FLAG$
```
![](/CTF-Hacker101/Easy/Images/Microv1-image1.png)

## Let's Begin

### Steps
1. We begin this CTF with two bulletpoint links and one 'Create the page' link. So where do we start?
   We start by clicking around and inspecting the page source of course.
   
![](/CTF-Hacker101/Easy/Images/Microv1-image2.png)

3. Let us click on the first link we see 'Testing'. We do not see anything out of the ordinary. From the page itself.
   Inspect source does not detect anything weird. So we will click on 'Edit this page' to see what else is there.
4. From here we can see a box, just below that something eye catching. *Markdown is supported, but scripts are not*
5. There is our first clue, script or better yet XSS script. You may want to google search more on this. But I done the work here.
   From searching we will want to create an script that will give us a pop-up alert. Choose one of them:
```html
<script>alert(document.domain)</script>
<script>alert(window.orgin)</script>
<script>alert(1)</script>
```
![](/CTF-Hacker101/Easy/Images/Microv1-image3.png)

5. Enter the script into the Title or Body and submit. Now you can go back home or refresh the page.
   You should see the alert pop up with the flag. Go ahead, copy, and submit it.
   
![](/CTF-Hacker101/Easy/Images/Microv1-image4.png)
   
<Code>Flag 1/4</Code>

6. Hey! What is this in the 'Elements' I see. In the url it say I am on page 11. Expanding the other  tags.
   I can see there is page 1 & 2. Super weird.

![](/CTF-Hacker101/Easy/Images/Microv1-image5.png)
   
7. We will start by checking other pages by replacing the numbers. Moving downwards and get to
    page 4 it says 'Forbidden', while the others were 'Not Found' .
9. How do we view this part, we will add to the URL edit/ in front of page/. So should be /page/edit/4 at the end of the URL.
10. Once you press enter, you will be reveal another flag on this page. Go ahead and submit the flag.

![](/CTF-Hacker101/Easy/Images/Microv1-image6.png)

<Code>Flag 2/4</Code>

11. This one I used hint to know where to start. The hint reveals that injection doesn't have to be only form submission. It can be done on the URL. Which I didn't know that. So to do this need to test SQL vulnerability.
12. Click on any of the links on the page. Then put a quotation '`' next to the page number. Once you press enter, another flag appear.
    Go ahead and submit that.

![](/CTF-Hacker101/Easy/Images/Microv1-image7.png)

<Code>Flag 3/4</Code>

13. Now we need to find the last flag. This one, I had to ask for help. I reach out to a random discord member who had done this. They pointed out that I need to look into something called [**XSS Filter Evasion**](https://cheatsheetseries.owasp.org/cheatsheets/XSS_Filter_Evasion_Cheat_Sheet.html)

14. There is a lot going on but using the previous script we did, we will look for one that provide us alerts. Which I done for you.
    You have to option. Either one works, but I prefer the later, you will see why when you test it out.
```html
<IMG SRC= onmouseover="alert('xxs')">
<IMG onmouseover="alert('xxs')">
```
15. You will edit the page, that says 'Markdown Test'. Same as the first flag, copy and paste the code below the broken image source.
    Save the changes. You will notice nothing pops up even if you refresh. This is because it will show up in your source page.     
    Inspect the page source. Expand the tags, and you will see the flag populate on the 'Elements'. Submit that and we completed the 
    challenge.

![](/CTF-Hacker101/Easy/Images/Microv1-image8.png)

<Code>Flag 4/4</Code>

### Conclusion
This challenge was more tricky than the trivial ctf. There were two flags that I had to use hints or reach out to someone.
I learn is don't be afraid to reach out or look at other walk-through in the beginning. It is a learning experience, so don't just copy and call it a day. Try to understand what was the method use and how they solve it. Write it down and use that knowledge on the next CTF. Eventually you will get better at it. 

