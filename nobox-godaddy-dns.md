Guide: Setting up your GoDaddy domain for Nobox Web Hosting
===========================================================

1) Start by logging into your GoDaddy account.

2) Once logged-in, click on the top right `My Account` CTA and select the `Manage My Domains` option on the leftmost area of the menu that just appeared.

![Nobox web hosting for GoDaddy domains](http://i.imgur.com/Bf8Zmjl.jpg)

3) Now, on the `Domains` control panel, select the domain that we will direct to the Nobox Web Hosting server and click on its name. This will bring the `Domain Details` panel forward.

![Nobox web hosting for GoDaddy domains](http://i.imgur.com/MXcGSSC.jpg)

4) Proceed to click on the `DNS Zone File` tab. In this panel view, we will accomplish 2 things. Setup the staging hosting area and setup the production area.

![Nobox web hosting for GoDaddy domains](http://i.imgur.com/ycqlFTT.jpg)

5) Click on the `Add Record` CTA.

![Nobox web hosting for GoDaddy domains](http://i.imgur.com/ofyFNeJ.jpg)

Select an `A (Host)` record type in the light box that will popup and fill in the information just like the screenshot below. Host: dev. Points to: `104.131.84.45`. When all fields are complete, press `Finish` to close the light box.

![Nobox web hosting for GoDaddy domains](http://i.imgur.com/cBrSbD5.jpg)

![Nobox web hosting for GoDaddy domains](http://i.imgur.com/E45xhKf.jpg)


6) Click on the `Edit` icon next to the 1st `A (Host)` record area.

![Nobox web hosting for GoDaddy domains](http://i.imgur.com/ofyFNeJ.jpg)

The edit light box will popup; proceed to fill in the information just like in the screenshot below. Leave `host` as-is, and change the `Points to` to `107.170.20.199`. When you are complete, press `Finish` to close the light box.

![Nobox web hosting for GoDaddy domains](http://i.imgur.com/vQuRl1C.jpg)


7) You’ll notice a red warning ribbon, follow the instructions on the ribbon and press `Save Changes`. If the red warning ribbon doesn’t appear, make sure to redo the steps above because the changes didn’t registered.


![Nobox web hosting for GoDaddy domains](http://i.imgur.com/UmmsWw9.jpg)

8) **Done**. When the DNS records refresh (usually within 2-24 hours) we’ll be able to serve both staging and production domains from our Nobox Web Hosting.
