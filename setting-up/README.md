![](../images/line3.png)

### Setting up Unreal & Perforce

<sub>[home](../README.md#user-content-ue4-intro-to-level-design) • [next](../camera-mechanics/README.md#user-content-lock-cameras-and-mechanics)</sub>

![](../images/line3.png)

We will be using Unreal's third person template as a starting point for our 3-D platforming game we will be using for level design.  This will give us all we need for a basic character that we can control with some tweaks to make it to our liking.  Lets start by creating a project in Unreal then using **Perforce** to store our work.

<br>

---


##### `Step 1.`\|`UE5LD`|:small_blue_diamond:

If you have not installed the required software go and add [Epic Games Launcher](https://www.epicgames.com/store/en-US/download) and [P4V](https://www.perforce.com/downloads/helix-visual-client-p4v) - this assumes you have a **Perforce** server which is free if you are team of 4 people or less and can be found at [Perforce Helix Core](https://www.perforce.com/products/helix-core/free-version-control).  Make sure you have installed **Unreal** version `5.2.x` so that you will be compatible with this walk through. 

Run the **Epic Games Launcher** and Press **Launch** button to launch the editor.

![screenshot of epic game launcher](images/image_01.png)

![](../images/line2.png)

##### `Step 2.`\|`UE5LD`|:small_blue_diamond: :small_blue_diamond: 

You can pick from different starting templates with Games, Film/Video & Live Events, Architecture and Automotive Product Design & Manufacturing as options.  You can also load recent projects as well!

We are going to make a game so lets start by selecting **Games** and then select the **Third Person** template.  

The first settings on the top right is set to **BLUEPRINT**.  You can select between **C++** and **BLUEPRINT**.  Since we will not be doing any C++ programming in this exercise we will leave it with Blueprint.  I am leaving the **Target Platform** as **Desktop** and the **Quality Preset** to **Maximum Quality** as we are developing this for a modern computer.  We do not need the starter content so we will set the **Starter Content** to `false` to keep our project size at bay. We will leave **Raytracing** off as we will not be using it at the moment.  

Select your **Perforce** workspace as the folder to save the project in and call it `IntroToLevelDesign`.  Press the <kbd>Create</kbd> button to start the game with the third person template.

![Unreal Select or Create New Project screen](images/image_03.png)


![](../images/line2.png)

##### `Step 3.`\|`UE5LD`|:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

In the editor select the **Edit** menu item then from the drop down menu select **Editor Preferences**. Select **General | Loading & Saving** tab from the left hand side.  Go to *Source Control* and set **Prompt for Checkout on Asset Modification** and **Add New Files when Modified** to `true`.  Leave the other two settings with their default setting. 

![select third person ue4 template](images/image_17.png)

![](../images/line2.png)

| `version.control`\|`Introduction To Level Design`| 
| :--- |
| :floppy_disk: &nbsp;&nbsp;Version control saves lots of space on our laptops so that all project data can be safely backed up and saved on the server but we only need the assets we are currently using on our local hard drive.  It is also good practice as most game projects use some form of version control. It is absolutely necessary on team projects.  In this case we will be using **Perforce's Helix Core** server. |

![](../images/line2.png)

##### `Step 4.`\|`UE5LD`|:small_blue_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

Now go back to the game editor screen and press **File | Save All** then **File | Exit** to quit **Unreal**.

![save and quit Unreal](images/quitUE.png)

![](../images/line2.png)

##### `Step 5.`\|`UE5LD`| :small_orange_diamond:

Now lets log into **P4V** with your server address and user name. You also need to select the **Workspace** you are using.  Press the <kbd>OK</kbd> button.  

Remember this is the local version of the project.  When you **Submit** you update the **Depot**. You might need to press refresh but now you should see the **IntoToLevelDesign** folder. You can see the `.uproject` file and there is no icon so it has not been submitted to the **Depot** yet.

![Login and look at P4V](images/image_05.png)

![](../images/line2.png)

##### `Step 6.`\|`UE5LD`| :small_orange_diamond: :small_blue_diamond:

One last step we need to take care of is that we need to make sure we have a ``.p4ignore` file in th e root folder of our project.  We should also have a `p4config`. This should contain basic information about our Perforce setup for this class.   Please note that you might need to make adjustments to your default settings to see hidden files.  `.p4ignore` is a hidden file.  Any file without a prefix before the extension is hidden by default. Go to [Microsoft Help](https://support.microsoft.com/en-us/windows/show-hidden-files-0320fe58-0117-fd59-6851-9b7f9840fdb2) to find out how to alter your settings.

If you do not have a config file go to the file explorer and run `setconfig.bat` again.

![ensure .p4config is set up properly](images/p4ignore.png)

![](../images/line2.png)

##### `Step 7.`\|`UE5LD`| :small_orange_diamond: :small_blue_diamond: :small_blue_diamond:

Now lets make sure everything works as it should.  Go to any file in the root folder and right click and select **Open Command Window Here...**. Then type `p4 set` and you should see that is referencing the settings in your `.p4config` file.

![run p4 set](images/p4set2.png)

![](../images/line2.png)

##### `Step 8.`\|`UE5LD`| :small_orange_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

Now if we double click on the `.p4ignore` file and look at it in a text editor it indicates which files get submitted to source control and which don't. In our game folder we have our **Config** and **Content** folder which contains all of the unique portions of the game.  Most of the other folders like **Binaries/**, **Saved** and **Intermediate** are compiled to each person's computer for the game.  So these can be deleted then recreated when the game is run.  These do not need to be added to source control as it is uneeded tracking of dynamically generated content.  

![contents of .p4ignore file](images/p4ignoretext.png)

![](../images/line2.png)

##### `Step 9.`\|`UE5LD`| :small_orange_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

Now we need to add these files to the database and to the **Depot** (server).  Select the very top folder that contains the `.uproject` file (in my case it is called **Intro to Level Design**. We then want to add all new files. We do this by pressing thge <kbd>+ Add</kbd> button.  We then select a **New** changelist and add a message. All we did was create a default project so I used `Default third person project`. When you are done press the <kbd>OK</kbd> button.

![add files to perforce](images/addFilesToP4.png)

![](../images/line2.png)

##### `Step 10.`\|`UE5LD`| :large_blue_diamond:

Now press the <kbd>Submit</kbd> button to send these local files to the **Depot** on the server.  The first pop-up will show the ignore file working.  It should list the files not marked for add.  This is exactly what we want.  If you don't get this go back to the previous step and make sure your `.p4ignore` is set up correclty. Press the <kbd>OK</kbd> button to continue.

![files being ignored by submit](images/listIgnoreFiles.png)

![](../images/line2.png)

##### `Step 11.`\|`UE5LD`| :large_blue_diamond: :small_blue_diamond: 

Now you will get a list with all the files you want to submit in the **Changelist** with the message you previously entered.  Make sure that all of files being submitted are all in the **Contents** or **Config** folders as well as the `.uproject` file. When you are happy press the <kbd>Submit</kbd> button.

![list of files to submit](images/submit.png)


![](../images/line2.png)


##### `Step 12.`\|`UE5LD`| :large_blue_diamond: :small_blue_diamond: :small_blue_diamond: 

Press the <kbd>Refresh</kbd> button in **P4V** and you will see that files in the **Content** folder have a green icon.  Files in the **Intermediate** folder do not.  So our `.p4ignore` is working corretly.  For icon meaning check out the [P4 Icons](https://github.com/maubanel/p4v-unreal/blob/main/icons/README.md#user-content-p4v-icons).

![setup github repository](images/filesSaved.png)

![](../images/line2.png)

##### `Step 13.`\|`UE5LD`| :large_blue_diamond: :small_blue_diamond: :small_blue_diamond:  :small_blue_diamond: 


Run the game while you are still logged into **Perforce**.  It is best practice to double click the `.uproject` name to load it. This will now run **Unreal** and you are certain it is from the **P4** folder you are tracking.

![run game](images/loadGame.png)

![](../images/line2.png)

##### `Step 14.`\|`UE5LD`| :large_blue_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:  :small_blue_diamond: 

Now we can use the engine to do our future source control submissionms.  Press the **Source Controll Off** item at the bottom right of the window.

Select `Perforce` as the **Provider** and enter the **Server** address.  Enter your **Username** and the name of your **Workspace** (this can be selected from the **Available Workspaces** drop down menu).

Press the <kbd>Accept Settings</kbd> button.  You should see a pop up on the bottom right saying that it was succesfully connected to source control.

![select source control](images/selectSourceControl.png)

![](../images/line2.png)

##### `Step 15.`\|`UE5LD`| :large_blue_diamond: :small_orange_diamond: 

Download a thumbnail that you can use on this project [Intro Thumbnail](images/IntroToLevelDesign.png). Press the **Settings** button and select **Project Settings**.  Press the three dots in the **About | Project Thumbnail** tab next to the thumbnail and attach the `IntroToLevelDesign.png`.

![add Intro to Level design logo](images/introToLD.png)

![](../images/line2.png)

##### `Step 16.`\|`UE5LD`| :large_blue_diamond: :small_orange_diamond:   :small_blue_diamond: 

Enter a **Description**, **Project Name**.  Put your name as the **Publisher | Company Name** and you can add your email in **Support Contact**. Add the **Project Displayed Title** and **Project Debug Title Info**. I also encourage you to select a legal claim on your work and paste it in the **Copyright Notice**.  I publish all my classes as the MIT License.  Replace **Copyright Holder** with your name. 

>Copyright 2023 **COPYRIGHT HOLDER**<br><br>Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:<br><br>The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.<br><br>THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

![add information to project settings](images/customSettings.png)

![](../images/line2.png)

##### `Step 18.`\|`UE5LD`| :large_blue_diamond: :small_orange_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

Press play and lets see what we get? Run around using the **UP | DOWN | LEFT | RIGHT** keys on the keyboard. Press **Space Bar** to jump.  Get used to the controls - we will make some changes in the next section.

https://user-images.githubusercontent.com/5504953/175449850-b30e590b-9812-42d9-9a09-74a22943b66d.mp4

![](../images/line2.png)

##### `Step 19.`\|`UE5LD`| :large_blue_diamond: :small_orange_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

Select the **File | Save All** then press the <kbd>Source Control</kbd> button and select **Source Control...**. Enter a **Changelist Description** and then press <kbd>Submit Content</kbd>. Update the **Changelist Description** message and with the latest changes. Make sure all the files are correct and press the <kbd>Submit</kbd> button. A confirmation will pop up on the bottom right with a message about a changelist was submitted with a commit number.

![save all and submit to perforce](images/submitP4.png)

![](../images/line2.png)

##### `Step 20.`\|`UE5LD`| :large_blue_diamond: :large_blue_diamond:

Sometimes not all files get submitted to Unreal especially for files that don't show up in the editor.  It is good practice one you submit in **Unreal** and quit the game to right click on the top most project folder and select **Reconcile Offline Work...**.

This will either give a message saying ther is nothing to reconcile or bring up a tab.  Make sure that these are **NOT** files in the **Intermediate** and **Saved** folders as these should be ignored from the `.p4ignore`.

If the files are in **Content** or **Configuration** then press the <kbd>Reconcile</kbd> button.  Then submit the changes with a message and press the <kbd>Submit</kbd> button.

![reconcile offline work](images/reconcile.png)

![](../images/line2.png)

![next up lock camera and mechanics](images/banner.png)

![](../images/line.png)

| [home](../README.md#user-content-ue4-intro-to-level-design) | [next](../camera-mechanics/README.md#user-content-lock-cameras-and-mechanics)|
|---|---|
