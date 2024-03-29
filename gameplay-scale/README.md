![](../images/line3.png)

### Gameplay & Scale Register

<sub>[previous](../double-jump/README.md#user-content-double-jumping) • [home](../README.md#user-content-ue4-intro-to-level-design) • [next](../long-jump/README.md#user-content-long-jump)</sub>

![](../images/line3.png)

Lets finish our double jump and start creating a gameplay and scale register that we can use for level design to make sure that our placement of objects will be to scale and work with gameplay.

We will use this information to create more jump platforms.

<br>

---

##### `Step 1.`\|`UE5LD`|:small_blue_diamond:

Now in video games one of the most expensive portions is rendering graphics and resolving collisions.  For rendering graphics, the more polygons we have in the scene (especially the ones we see in the camera) the slower the framerate and the more processor and GPU will be used.

For collisions it comes down to shape complexity and how many objects in the scene need to be checked for collision. The more complex the shapes the more places we have to check on the two models potentially colliding to see if there is an actual collision.  So in games we try and use "cheap" collisions as much as we can.  

So visually we have a very detailed chair model but the purple lines in the default Unreal chair is a very simple shape.  This is done primarily for performance (to get a decent framerate) but also for physics.  If the player is to alk on the back or arms of the chair, a flat shape is prefered (so you don't always slide off).

![collision for chair](images/CollisionAndMesh.jpg)

![](../images/line2.png)

##### `Step 2.`\|`UE5LD`|:small_blue_diamond: :small_blue_diamond: 

So for our player the most common collision detection is with the ground to unsure they should be running/walking instead of falling. This is done every frame and it doesn't look at the foot model of the character.  It uses a very simple **capsule** (a cylinder with two hemispherical ends). 

For a player collision a simple shape that provides satisfactory collision ends up being a capsule.  A box collider would have edges and the player wouldn't move smoothly along edges when jumping or when climbing stairs.

![capsule and cube collision examples](images/capsuleCube.png)


![](../images/line2.png)

##### `Step 3.`\|`UE5LD`|:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

So whe figuring out how far and high we can jump, we do not measure the player but we measure the player's collision volume.  This is what determines where the player collides in the world. So if the collision volume doesn't pass through the player won't.  This is the **Capsule Component** in the player blueprint.  This is what we are measuring for. 

Now this collision volume is NOT visible in game as the player doesn't even know it exists.  Lets see it, which will help us in level design as it is all abou collision volumes.

Go to to **Third Person Character** and press on the **Capsule Component**.  Look for **Rendering** and turn **Hidden in Game** `off`. This way we can see the capsule collider in game which will help with grey blocking.

![turn hidden in game off](images/hiddenInGame.png)


![](../images/line2.png)

##### `Step 4.`\|`UE5LD`|:small_blue_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

Now lets imagine that we have tested and tweaked the physics to be exactly what we wanted (we do want to lock player physics before begining an actual level gray block).  So we can establish some scale and gameplay metrics and enter it into our register.

We need to know the size of the player to know what it can fit in and what it can't can't.  This dictates minimum size for doors and other objects we want to craft.

We can easily measure scale by going in the editor and putting a player in the level (don't forget to remove them after) and change to an orthographic view like **Front** or **Left**.  I like putting it in **Wireframe** view as well to be extra accurate. Hold the middle mouse button (can't seem to do this on a touchpad) and drag from one end to the other and you will get the result in unreal units (uu/cm).

![measure width and height of player](images/measurePlayer.png)

![](../images/line2.png)

##### `Step 5.`\|`UE5LD`| :small_orange_diamond:

Now if we walk our player up to the wall when we press play we can confirm these measurements and they look accurate right next to the material that is a square meter in size.

Now then we have the first entry in our Scale Register. Since uu's default to cm we will stick with the metric system from now on. The player is 1.79 meters tall (~5' 10") and a width and depth of .71 m (~2' 4").

**Scale Register**
|Item|Dimensions|
|-------------|-------------|
|Player Height | 1.79 m|
|Player Width | .71 m|

![player 179 cm tall by 71 cm wide ](images/heightWidthPlayer.png)

![](../images/line2.png)

##### `Step 6.`\|`UE5LD`| :small_orange_diamond: :small_blue_diamond:


We now can go into the game and jump and double jump and measure roughly the distances that we can make from standing.

**Gameplay Register**
|Element | Measure|
|-------------|-------------|
|Single Jump | ~200 |
|Double Jump | ~410|

![jump height and double jump height added to register](images/jumpHeight.png)

![](../images/line2.png)

##### `Step 7.`\|`UE5LD`| :small_orange_diamond: :small_blue_diamond: :small_blue_diamond:

Now lets double jump and see if we have enough clearance without adjusting the camera up or down.  In my case my camera can still clip the top of the platform ceiling which causes a glitch.

![camera in default position clips with ceiling](images/camOverlap.png)

![](../images/line2.png)

##### `Step 8.`\|`UE5LD`| :small_orange_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:
Lets fix this. Remake the first platform to be 1200 cm tall with a center 950 cm opening instead of the original 1000cm/775cm. We can now add this to our scale register. We will create an opening to jump through that is 9.5 meters.

**Scale Register**
|Item|Dimensions|
|-------------|-------------|
|Player Height | 1.92 m|
|Player Width | .84 m|
|Double Jump Opening Height | 9.5 m|

Create a new cube that is a **Width** of `400`, **Depth** of `800` and **Height** of `1200` with **Align to Normal** set to `false`.  Create an inner box to cut away a hole with a **Width** of `775`, **Depth** of `408` and **Height** of `950`. Select **PolyModel | Mesh Bool** and subtract the inner shape.  Press the <kbd>Accept</kbd> button. Assign the `M_LDGrid_Local` material to the box.

![create a new jump platform that is 400 x 800 x 1200](images/redoFirstJumper.png)

![](../images/line2.png)

##### `Step 9.`\|`UE5LD`| :small_orange_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

Now lets delete the old smaller jump platform.  You can then press press the <kbd>Force Delete</kbd> button.

![delete the old shape and replace it](images/deleteReplace.png)

![](../images/line2.png)

##### `Step 10.`\|`UE5LD`| :large_blue_diamond:

Delete the old shapes from the **Content Drawer** and move the **Static Mesh** to the **Meshes** folder.  Selet **Content** and right click then select **Fix Up Redirectors in Folder**. Now rename the file back to the original `SM_JumpPlatformLow`.

![rename file to SM_JumpPlatform_Low](images/rename.png)

![](../images/line2.png)

##### `Step 11.`\|`UE5LD`| :large_blue_diamond: :small_blue_diamond: 

Run the game and notice that we can now double jump and don't have the camera hit the top of the platform.  We are done with our low example.

https://user-images.githubusercontent.com/5504953/182050177-c135a839-cbd3-4b28-ae7c-52bb49cabda8.mp4

![](../images/line2.png)

##### `Step 12.`\|`UE5LD`| :large_blue_diamond: :small_blue_diamond: :small_blue_diamond: 

Our first jump platform we created was about 110 uu units high (1.1 meters).  The player can easily clear it with a single jump. Now lets make two more jump platforms.  One that can just clear a single jump.  And one that can just clear a double jump. For these you will have to make positions that reflect our gameplay register.

**Gameplay Register**
|Element | Measure|
|-------------|-------------|
|Single Jump | ~200 |
|Double Jump | ~410|

Lets create a platorm (**Shapes | Box**)with a 2 meter height so a **Width** of `400`, **Depth** of `800` and **Height** of `1300`.  Assign the **M_LDGrid_Local** material to it.  Then create another **Shaped | Box** for a hole that is a **Width** of `775`, **Depth** of `408` and **Height** of `850`.  Now do a **Difference** operation on **PolyModel | MshBool**. Press the <kbd>Accept</kbd> button after each stage. Place this platform to the right of the prior one. 

Clean up the directory and name it `SM_JumpPlatform_Mid`. If the first jump was tricky - this jump is hard to make with a single jump but not impossible. Run the game and test your work.  In my case I can easily clear the platform with a single jump.

https://user-images.githubusercontent.com/5504953/182051619-0caaf950-2f97-465d-a40f-d261ea3c0647.mp4

![](../images/line2.png)

##### `Step 13.`\|`UE5LD`| :large_blue_diamond: :small_blue_diamond: :small_blue_diamond:  :small_blue_diamond: 

Now lets create a jump height of 4 meters.  Lets call it `BR_JumpPlatform_Tall`.  I will let you do this on its own.  Then press run and double jump over the platform. You need to ensure that you can only clear it with a double jumnp. Call it `SM_DoubleJumpPlatform`.

https://user-images.githubusercontent.com/5504953/182051795-244c175e-b02e-4f50-9cbe-7679c60c098f.mp4

![](../images/line2.png)

##### `Step 14.`\|`UE5LD`| :large_blue_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:  :small_blue_diamond: 

Create a new folder called **Jump Platforms** and move the three platofmrs in it.  Name them correctly in the **World Outliner**. Also, make sure you have the three meshes correclty named in the **Meshes** folder. Delete all cutter and unused meshes you created.

![convert two brush platforms to static mesh](images/renamedJumpPlatforms.png)

![](../images/line2.png)

##### `Step 15.`\|`UE5LD`| :large_blue_diamond: :small_orange_diamond: 

Press the **Add Asset** button and select the **All Classes | Text Render** for a title to sit above the jump platforms. Position and rotate it and change the **Text** to `Jump Platforms`.  Make a **World Size** of `240` and a color that contrasts with the sky. Name them correctly and place them in the **Jump Platforms** folder.

![create jump platform text title](images/jumpPlatformText.png)

![](../images/line2.png)

##### `Step 16.`\|`UE5LD`| :large_blue_diamond: :small_orange_diamond:   :small_blue_diamond: 

Once you are happy with the position select both titles and hold <kbd>Alt</kbd> while selecting the letters to make a copy.

![duplicate and name title](images/dupePlatforms.png)

![](../images/line2.png)

##### `Step 17.`\|`UE5LD`| :large_blue_diamond: :small_orange_diamond: :small_blue_diamond: :small_blue_diamond:

Call this second title **Ramp** and place it in the **Ramp** folder and alter the name in the **World Outliner** to properly reflect the new function.

![Add jump platforms text on top of jump platforms](images/rampTitle.png)


![](../images/line2.png)

##### `Step 18.`\|`UE5LD`| :large_blue_diamond: :small_orange_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

Select the **File | Save All** then press the <kbd>Source Control</kbd> button and select **Source Control...**. Enter a **Changelist Description** and then press <kbd>Submit Content</kbd>. Update the **Changelist Description** message and with the latest changes. Make sure all the files are correct and press the <kbd>Submit</kbd> button. A confirmation will pop up on the bottom right with a message about a changelist was submitted with a commit number.

![submit work to Perforce](images/CommitWork.png)

![](../images/line2.png)

##### `Step 19.`\|`UE5LD`| :large_blue_diamond: :small_orange_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

Sometimes not all files get submitted to Unreal especially for files that don't show up in the editor.  It is good practice one you submit in **Unreal** and quit the game to right click on the top most project folder and select **Reconcile Offline Work...**.

This will either give a message saying ther is nothing to reconcile or bring up a tab.  Make sure that these are **NOT** files in the **Intermediate** and **Saved** folders as these should be ignored from the `.p4ignore`.

If the files are in **Content** or **Configuration** then press the <kbd>Reconcile</kbd> button.  Then submit the changes with a message and press the <kbd>Submit</kbd> button.

![reconcile offline work](images/Reconcile.png)

![](../images/line.png)

<!-- <img src="https://via.placeholder.com/1000x100/45D7CA/000000/?text=Next Up - Long Jump"> -->
![next up next tile](images/banner.png)

![](../images/line.png)

| [previous](../double-jump/README.md#user-content-double-jumping)| [home](../README.md#user-content-ue4-intro-to-level-design) | [next](../long-jump/README.md#user-content-long-jump)|
|---|---|---|
