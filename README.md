CS52 Workshops: Chrome Extensions!!!!!!!!
====================
![](https://i.imgur.com/4DXxPO6.png)

Overview
---------------------
This tutorial will teach you how to setup a basic Chrome Extension that displays a specified background image upon loading a certain page.



Let's go! 
---------------------
### Step 1: Make a directory in terminal (name it however you like!)

    mkdir 4_28_chrome_extension
    
### Step 2: Create manifest.json file and open it:

    touch manifest.json

This `manifest.json` file is necessary for every chrome extension. It holds the metadata on the extensions's information, such as title, description, etc.

Open `manifest.json` and paste this code into the file: 

    {
        "manifest_version": 2,
        "name": "Custom Google Homepage",
        "description": "This extension does shows a picture upon navigation to Google",
        "version": "1.0",

        "page_action": {
        "default_title": "My custom google page!"
        }
       }


### Step 3: Connect extension to Chrome 
1. Go to **chrome://extensions**
2. Toggle on the the "developer mode" in the upper right corner as shown below:

![](https://i.imgur.com/WWFnigM.png)

### Step 4: Click "Load Unpacked" and select your directory
This step is to check that the `manifest.json` file can be loaded correctly as an extension in your browser. If there are any errors, it will be displayed (ie missing a file, cannot read,etc). If there are no errors, the extension will load automatically.

Toggle the checkbox in our extension to make sure it is on. 

![](https://i.imgur.com/buUQyqX.png)

Yay! now your extension should be loadable.

### Step 5: 
Add content scripts to the manifest.json after "version": and before "page_action"{

    ,
    "content_scripts": [
        {
        "matches": ["https://www.google.com/*"],
        "css": ["main.css"]
        }
        ],

The Matches part refers to the URL what we want our extension to modify/personalize. Here, we are setting it to google.com. We can link other files to content scripts. 
Since we want to change the background, let's add a css file.

### Step 6: Create the CSS file!

    touch main.css

In this case, we want our personalized page to have unique background:


    body#gsr.hp.vasq{
        background-image: url("https://wallpaperaccess.com/full/1331874.jpg");
       }
       div.gb_xe.gb_R.gb_Me.gb_Ee {
        font-weight: bold;
        font-size: 15px;
       }

Feel free to change the url to whatever picture you would like. Just make sure the url is of an image only.
At this point if you unpack your extension again and navigate to google.com you should have this beautiful backdrop:
  ![](https://i.imgur.com/tH0wwLU.jpg)
Woohoo!

### Step 7: Add a Browser Action popup:

Add this to your `manifest.json` under content scripts:

    "browser_action": {
    "default_title": "My personalized google page!",
    "default_popup": "popup.html",
    }
    
What this is doing is creating a browser action in the toolbar (seen to the right of the address bar). A browser action can have a tooltip, icon, badge, and popup. Here, we want to make a popup, and so there there is a specification for the popup title and source.

* *Fun Fact:* Similar to browser actions are page actions, where the extension icon lights up and the page actions have functionality only when the user is on the specified page url, matched in the content script. See 'More on Page Actions' under **Resources** at the bottom of this page for more info! Browser actions differ from page actions because they are enabled on all tabs and URLs. 

We are going to make a popup for our browser action! Popups will display upon clicking the icon (default is the puzzle piece). Since this is for a browser function, this popup will display no matter what page you are on!

The copied text above tells `manifest.json` to read the information for the popup from popup.html, so let's create it! 

Create a `popup.html` file:

    touch popup.html 

Inside your `popup.html` file, add the following code (feel free to edit the body and make it a bit more original :) :

    <!DOCTYPE html>
    <link rel="stylesheet" type="text/css" href="popup.css" />
    <link href='https://fonts.googleapis.com/css2?family=Josefin+Sans&family=Montserrat&family=Poiret+One&family=Spectral:wght@400;600&display=swap' rel='stylesheet'    type='text/css' />

    <html>
        <body>
            <h1>Go to google.com for a GOLDEN search experience!</h1>
            <img src="dog.jpg" height="140px" width="100px">
        </body>
    </html>

Let's add some *style* to this popup! You may have noticed that in the code above, we have added a CSS styling file, as well as some fonts. Feel free to modify as you wish. 

Make the file `popup.css`!

    touch popup.css

Now, styling time! Here is an example to get started. Feel free to make it personal!

    body{
        background-color: goldenrod;
    }

    h1{
        color: lightyellow;
        font-family: 'Poiret One', cursive;
    }

Now, when you reload your extension (load unpacked again) you should be able to click on the puzzle piece icon on any page and see your pop-up!

![](https://i.imgur.com/ctOrXUi.png)


### Step 8: You're done!!
1. Save your files
2. Go back to **chrome://extensions** in your browser
3. Press "load unpacked" and reload your directory
4. Navigate to google.com and bask in the majesty of this golden retriever (or whatever picture you specified)!!

![](https://i.imgur.com/ZQrwU8G.jpg)

## Reflection Questions:

1. What functionality would you implement in an extension that could help in the day-to-day? For that functionality, would you use a page action or browser action for your icon in the browser? 
<em>I think browser actions make sense because to take up that much real estate on a browser, having an extension that does stuff for many pages makes sense.
A weather extension could be interesting/useful? Or a schedule one where it loads your schedule in quickly? I feel like most of these will have already been done.</em>

2. Think about your favorite extension or a popular extension. Try to explain the features of the extension and how it was implemented. 
<em>Think about your favorite extension or a popular extension. Try to explain the features of the extension and how it was implemented. 
One of my favorite extensions is Eye Dropper, which allows a person to click anywhere on the screen and will tell you the color. I think it includes a color picker and is definitely a 
browser extension as opposed to a page one.</em>



**Resources:**
- More on Browser Actions: https://developer.chrome.com/extensions/browserAction
- More on Page Actions: https://developer.chrome.com/extensions/pageAction
- https://medium.com/@LindaVivah/the-beginner-s-guide-build-a-simple-chrome-extension-in-minutes-498308ea406a
- https://www.youtube.com/watch?v=YQnRSa8MGwM&list=PLRqwX-V7Uu6bL9VOMT65ahNEri9uqLWfS&index=7 
