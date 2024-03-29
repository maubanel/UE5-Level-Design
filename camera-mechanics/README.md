![](../images/line3.png)

### Lock Cameras and Mechanics

<sub>[previous](../setting-up/README.md#user-content-setting-up-unreal--github) • [home](../README.md#uuser-content-ue4-intro-to-level-design) • [next](../holodeck/README.md#user-content-setting-up-holodeck)</sub>

![](../images/line3.png)

Blocking out or **Gray Blocking** a level is standard practice in most level based video game genres.  It allows us to navigate and play through a space to judge game mechanics and decide if the level works or not.  There is no use to adding lots of custom great art, to then realize that the game play does not work as designed.  This allows us to test the interactivity first before adding artwork to a level.

Now the first step before gray blocking is to make a final decision on physics of our main controllable character.  How would I know how to place platforms without knowing how far the player can jump.  We also need a near final camera as it will need to fit or adapt to the environment you set up.  We will do a very quick version of this first step that sometimes takes months/years on novel mechanics design.

The same thing could be true of any other application.  Why not as an architect, build a very simple version of the structure and navigate it first.  See what you like and don't like about your rough draft.  Then when you are happy you can go back to your modelling software and prepare a final detailed structure.

In this case I am envisioning a third person platformer like **Mario** and we will customize the default settings to alter the behabior to be more appropriate for this genre. Lets take a quick look at defining our paramters.

<br>

---

##### `Step 1.`\|`UE5LD`|:small_blue_diamond:

Now open the **ThirdPersonCharacter** blueprint that you find in **Content | ThirdPerson | Blueprints | BP_ThirdPersonCharacter**. Make sure you are in the **Viewport** tab. Now click on the **Camera Boom** component.  It is the parent of the FollowCamera.  This acts as a spring so that when the camera collides with geometry it acts as a spring to keep the camera from going into geometry. This is represented with the **red** arrow in the editor.

![open the thirdpersonncharacter blueprint](images/followCam.png)

![](../images/line2.png)

##### `Step 2.`\|`UE5LD`|:small_blue_diamond: :small_blue_diamond: 

The camera is very tight to the player light an action shooter.  We want a camera that is a bit further away.  In our character blueprint there is a boom that adjusts the distance and angle of the camera from the player. Select the **Camera Boom** component.  Change the **Target Arm Length** to a number like `750`.  Then adjust the **Socket Offset | Z** value to a value like `218`. Now the camera is above and further away but is not rotated facing the player.  Lets fix that.

![pull camera away from the player](images/camBoomAdjustment.png)

![](../images/line2.png)

##### `Step 3.`\|`UE5LD`|:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:
Now select the **FollowCamera** component and adjust the **Rotation Y** to `345`.  This will pitch the camera down 15 degrees pointing towards the back of the player's head.

![rotate camera to face player](images/changeRotation.png)

![](../images/line2.png)

##### `Step 4.`\|`UE5LD`|:small_blue_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

Press **Compile** in the blueprint then run the game and run into the back wall to see that the spring arm stops (and the player sort of disappears).  We will fix that in a later lesson when we dig more into blueprints. For now you can see that our camera is further back and high up looking down at the player.

https://user-images.githubusercontent.com/5504953/175455582-938251d1-fb04-493d-8f6f-98a4b4d617a2.mp4

![](../images/line2.png)

##### `Step 5.`\|`UE5LD`| :small_orange_diamond:

Open up the **ThirdPersonCharacter** blueprint and select the **CharacterMovement** component.  This is where all the adjustments for player physics is held.  Let's first change the gravity.  We want a bit of moon like physics for **Gravity**. If you hover the cursor over **Gravity Scale** you will get a description of what it does.  The default is `1.75`. Let's make it more like the moon gravity and set it to `1.35`. The lower the number, the lower the gravitational force.

![adjust gravity for jump](images/gravityScale.png)

![](../images/line2.png)

##### `Step 6.`\|`UE5LD`| :small_orange_diamond: :small_blue_diamond:

Press the **Compile** button on the blueprint and run the game.  Now look at how the player's gravity changes and the player floats more when jumping. The physics feel like you are on the moon.

https://user-images.githubusercontent.com/5504953/175456397-6f38bba5-3469-4ea7-9e4d-57ac4dc9694a.mp4

![](../images/line2.png)

##### `Step 7.`\|`UE5LD`| :small_orange_diamond: :small_blue_diamond: :small_blue_diamond:

Lets make a few more changes.  Lets make our character run a bit faster.  In the blueprint change the **Character Movement: Walking | Max Walk Speed** to `800 cm/s`(the default was 500 cm/s). This will give us a more arcady quick feel. Play the game and tune the value to your liking.

![make player run faster](images/maxWalkSpeed.png)


![](../images/line2.png)

##### `Step 8.`\|`UE5LD`| :small_orange_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

Now lets make the player jump higher and give the ability for the player to adjust his direction mid flight.  In **Character Movement: Jumping / Falling** change **Jump Z Velocity** to `750.0` to make the player jump height. To give you more control in the air after you jump you can increase the **Air Control** to `0.5`. Play the game and tune the numbers to your liking. None of these numbers are \"correct\" or \"right\".  These are all up to you and how you want your character to move.

![make player jump higher and give them more air control](images/airControl.png)

![](../images/line2.png)

##### `Step 9.`\|`UE5LD`| :small_orange_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

Press the <kbd>Compile</kbd> button and play agian.  Now we can jump a little higher and have more control to change direction in air.

https://user-images.githubusercontent.com/5504953/175457618-432304c9-00d0-4c9f-8c4f-5b1045e05ae5.mp4

![](../images/line2.png)

##### `Step 10.`\|`UE5LD`| :large_blue_diamond:

It is sluggish when turning directions, we want a very snappy turn. We will adjust the **Character Movement (Rotation Settings) | Rotation Rate Z** to `1000`. Play the game and tune the numbers to your liking.

![adjust rotation rate of player character](images/rotationRate.png)

![](../images/line2.png)

##### `Step 11.`\|`UE5LD`| :large_blue_diamond: :small_blue_diamond: 

Play the game and make any changes to what I suggested.  Get the player to move the way you envision a player should move in an arcady third person game. It still feels a bit slugging when I start from idle.  I would like a faster acceleration.

https://user-images.githubusercontent.com/5504953/175459161-76916521-4e49-40d4-b0d0-3b98cb26d480.mp4

![](../images/line2.png)


##### `Step 12.`\|`UE5LD`| :large_blue_diamond: :small_blue_diamond: :small_blue_diamond: 

Go to **Character Movement | Max Acceleration** and change it to `3500.0`.

![adjust rotation rate of player character](images/maxAcc.png)


![](../images/line2.png)

##### `Step 13.`\|`UE5LD`| :large_blue_diamond: :small_blue_diamond: :small_blue_diamond:  :small_blue_diamond: 

Press the <kbd>Compile</kbd> button then play the game.  Now we have **much** snappier running.  The last final thing I don't like is the sliding when the player stops.  It makes it look like they are on ice instead of on ground.  Look carefully at the slow motion at the end of the video.

https://github.com/maubanel/UE5-Level-Design/assets/5504953/9a95c8d7-9f3b-493c-8159-46db5d58d304

![](../images/line2.png)

##### `Step 14.`\|`UE5LD`| :large_blue_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:  :small_blue_diamond: 

Increase **Character Movement | Walking | Breaking Deceleration Walking** to `5000` to slow down our player who has greater momentum to mimize the sliding at when the player stops.

https://github.com/maubanel/UE5-Level-Design/assets/5504953/509d9ae6-25b7-4818-85a7-e226d31baac6

![](../images/line2.png)


##### `Step 15.`\|`UE5LD`| :large_blue_diamond: :small_orange_diamond: 

Play the game and feel free to tweak any other settings and experiment to get the *feel* that you would like in your level.

https://github.com/maubanel/UE5-Level-Design/assets/5504953/067fa8ed-b5b9-4adf-a528-a6653b17655a

![](../images/line2.png)

##### `Step 16.`\|`UE5LD`| :large_blue_diamond: :small_orange_diamond:   :small_blue_diamond: 

Select the **File | Save All** then press the <kbd>Source Control</kbd> button and select **Source Control...**. Enter a **Changelist Description** and then press <kbd>Submit Content</kbd>. Update the **Changelist Description** message and with the latest changes. Make sure all the files are correct and press the <kbd>Submit</kbd> button. A confirmation will pop up on the bottom right with a message about a changelist was submitted with a commit number.

https://user-images.githubusercontent.com/5504953/175461700-1d8ef0ea-8174-47b8-9db4-96d80f5d7ae0.mp4

![](../images/line2.png)

##### `Step 17.`\|`UE5LD`| :large_blue_diamond: :small_orange_diamond: :small_blue_diamond: :small_blue_diamond:

Sometimes not all files get submitted to Unreal especially for files that don't show up in the editor.  It is good practice one you submit in **Unreal** and quit the game to right click on the top most project folder and select **Reconcile Offline Work...**.

This will either give a message saying ther is nothing to reconcile or bring up a tab.  Make sure that these are **NOT** files in the **Intermediate** and **Saved** folders as these should be ignored from the `.p4ignore`.

If the files are in **Content** or **Configuration** then press the <kbd>Reconcile</kbd> button.  Then submit the changes with a message and press the <kbd>Submit</kbd> button.

![reconcile offline content](images/reconcile.png)

![](../images/line.png)

![next up lock camera and mechanics](images/banner.png)

![](../images/line.png)

| [previous](../setting-up/README.md#user-content-setting-up-unreal--github)| [home](../README.md#user-content-ue4-intro-to-level-design) | [next](../holodeck/README.md#user-content-setting-up-holodeck)|
|---|---|---|
