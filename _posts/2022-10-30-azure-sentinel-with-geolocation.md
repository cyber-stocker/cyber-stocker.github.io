## Azure Sentinel with Geolocation


---

### Buckle up, here we go.

I went through [this](https://youtu.be/RoZeVbbZ0o0) lab a few weeks back, but nothing seems to be coming up when I run the Failed RDP with GEO Location command. Hmm, something is up. Let’s try and figure this out. 

First thing I want to double check is the settings are correct on my VM instance and to make sure that it is in fact accessible to the internet. 
I created a firewall rule when launching the VM that allows all inbound connections. I double check that is correct under “Networking” in the honeypot VM. Looks good! 

Alright, wait a minute. Clicking around in Azure I went into Sentinel and then clicked on the purple “Security” and after searching for “Security Event” and see over 38,000 events. Viola! Here is all my failed log in attempts. 38,000 is far more than zero. But where did I go wrong in the mapping of these events? Because when I use the custom Failed GEO Location search feature nothing is coming up. Something must have gone wrong when I “trained” the analytics with the log file. 
I went diving back into my Custom logs in my log analytics workspace. It’s there. I remember that the file we pull the data from is on the VM, not on my own computer. I had created a text file in notepad when I first did the lab containing the failed log in data used to train the analytics with. 
Let me try deleting it and starting this part again. 
I re-entered the path name. I think this may be where things went south. 
I tried re-training the analytics and now it is giving me an error when I try and parse out the log data (latitude, longitude, etc). I think it’s time to tear down and begin again. Azure credits, don’t fail me now! 

I attempt to log into the VM via RDP to see if it generates an alert.
When I create the new workbook and enter the script to pull the data to the map, the option to edit the map isn’t popping up for me. I’m thinking I need to give it a little time to gather some new data. I will come back and check it tomorrow.

_The next day

AHH!! Success. When I selected my workbook in Sentinel the map editing options popped up right away, and voila! My pretty map is displaying. It does limit me to 15 API calls a day, so the map is a bit underwhelming at the moment. [Here she is, large and in charge.](https://user-images.githubusercontent.com/113474900/198899244-55b87b39-90a5-4ac5-80f9-8611814d327e.jpg)


In re-doing the project from scratch, I suspect where I went wrong was in entering my own API key to covert the IP address to logitude and latitude. I’m not sure if I didn’t enter it correctly, or I failed to save the PowerShell script after entering it in. In the end, I am glad I was ultimately able to complete the lab. 

