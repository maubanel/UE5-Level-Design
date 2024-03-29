![](../images/line3.png)

### Moving Platform

<sub>[previous](../long-jump/README.md#user-content-long-jump) • [home](../README.md#user-content-ue4-intro-to-level-design) • [next](../moving-platform-ii/README.md#user-content-moving-platform-ii)</sub>

![](../images/line3.png)

Now a level will not be interesting unless we can allow you to exploit vertical height to make more interesting levels.  We need a moving platform that can get the player around the level!  Lets create a simple blueprint that allows us to have a moving platform that we can use in a variety of scenarios.

<br>

---


##### `Step 1.`\|`UE5LD`|:small_blue_diamond:

Copy the jump ramps title by select both actors then **Alt** dragging a copy to the right.  Call this new title `MovingPlatform1` & `MovingPlatform2`.  Add a folder called `Moving Platform`. 

![Add moving platform title to level](images/movingPlatformTitle.png)

![](../images/line2.png)

##### `Step 2.`\|`UE5LD`|:small_blue_diamond: :small_blue_diamond: 

AddSMPlatformAsset

Go back to **Modeling Mode** and select a **Shapes | Disc**.  Set the **Radius** to `300` and **Radius Slices** to `90`. Place it in the level and make sure the **Rotations** are all set to `0`, `0`, `0`. Press the <kbd>Complete</kbd> button.

![add M_AssetPlatform Asset to Scene](images/radialSlices.png)

![](../images/line2.png)

##### `Step 3.`\|`UE5LD`|:small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

Now you can select **PolyModel | PolyEd** and select **Extrude**.  Now give the platform some depth and press the <kbd>Accept</kbd> button.

![extrude face](images/extrudePolys.png)

![](../images/line2.png)

##### `Step 4.`\|`UE5LD`|:small_blue_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

Another way of adding a material is to drag it on the static mesh.  Drag and drop **MD_LDGrid_Local** on the disc to give it the scaled material.

![Add material to disc](images/addMaterial.png)

![](../images/line2.png)

##### `Step 5.`\|`UE5LD`| :small_orange_diamond:

Move the **PlayerStart** actor next to the platform with the red arrow pointing at it. Now rename the disc to `SM_MovingPlatform` and drag it into the **Meshes** folder. Then rename the platform and move it into the correct folder in the **World Outliner**.

![move player start next to platform](images/playerStart.png)


![](../images/line2.png)

##### `Step 6.`\|`UE5LD`| :small_orange_diamond: :small_blue_diamond:

Return to **Selection Mode** and run the game and you can jump on the platform.  Make any changes you see fit, but I am happy with mine! 

https://github.com/maubanel/UE5-Level-Design/assets/5504953/3e171c6d-7bdf-4be4-b5c6-1ae68b98cfcd

![](../images/line2.png)

##### `Step 7.`\|`UE5LD`| :small_orange_diamond: :small_blue_diamond: :small_blue_diamond:

Now we don't want to create a single platform in this level.  We want to create a game actor that we can use multiple times in multiple levels.  In Unity these are called **Prefabs**, in Unreal we use **Blueprints**.  

Go to the **Blueprints** folder and *right click* in an open area and add a **Blueprint Class**. select . Now select an **Actor** blueprint (this is the base class for any object to appear in a level). Call this new **Blueprint** `BP_MovingPlatform`.

![turn actor to blueprint and call it BP_Platform](images/createBP.png)

![](../images/line2.png)

##### `Step 8.`\|`UE5LD`| :small_orange_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

Now open up **BP_MovingPlatforms**.  Sometimes when you open a blueprint you get just a partial display of the variables.  All you need to do is press the **Open Full Blueprint Editor**.  Now go to the **Viewport** tab and press the **+ Add** component button.  Select a **Static Mesh** component and rename it to `Jump Platform`.

![open blueprint and add component](images/openBPAddComponent.png)

![](../images/line2.png)

##### `Step 9.`\|`UE5LD`| :small_orange_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

Assign the **LD_Grid_Local** material to **Element 0** so we can see the nice measurement grid on the sattic mesh.

![open blueprint and add component](images/assignMaterial.png)

![](../images/line2.png)

##### `Step 10.`\|`UE5LD`| :large_blue_diamond:

I like docking the blueprint next to the editor if I am on a single monitor. Put the **BP_Platform** actor in the **Moving Platform** folder to join the titles.

![dock blueprint and put in moving platforms folder](images/bpPlatform.png)

![](../images/line2.png)

##### `Step 11.`\|`UE5LD`| :large_blue_diamond: :small_blue_diamond: 

We need to locations for the platform to move **From** and to move **To**.  We will just be translating the object and are not rotating or scaling it.  So we need an **X**, **Y**, **Z** float to store the location.  There is a data structure called a **Vector** available to us in Unreal.  It is a **struct** that holds the three floats we need. We need to create a Variable to store it.

Press the **+** button next to **Variable** and create a new Variable called `StartingPosition` of type **Vector** and make it **Private** and **Instance Editable**.  Put it in **Category** `Moving Platform` (since this category doesn't exist you will have type over the existing one to creat it) and give it a **Description** of `Starting location of the platform`.

We set **Private** to `true` as we want to default Variables to private to this object.  We would need to make it public if we wanted another actor to access the data. In this case we don't need to do this.  If you don't know, make the variable private.

The **Instance Editable** allows us to adjust this value in the game window to tune while playing the game.  This allows us to edit it in the game editor without going back to the blueprint.

We set a description as it allows us to get a tooltip when we highlight the variable in any place of the editor, cool!

![create startingPosition variable](images/startingPosition.png)

![](../images/line2.png)


##### `Step 12.`\|`UE5LD`| :large_blue_diamond: :small_blue_diamond: :small_blue_diamond: 

Now we want to be able to place the platform in the level and set this starting position.  We will create a function to make this easier to do.  A function is like a factory, it will do a job for us and give us something back.  Press the **+** plus button next to **Functions** and call it **Set Start Position**.  This will open up another graph to program the logic for this function.

Drag and drop the **Starting Position** variable and we want to read it so select **Get**.  Right clik on the open graph and select **Get Actor Location**.  This will allow us to access the current location of the platform and save it as the starting position!

![create a new function called set start position](images/createFunctionForSettingStart.png)

![](../images/line2.png)

##### `Step 13.`\|`UE5LD`| :large_blue_diamond: :small_blue_diamond: :small_blue_diamond:  :small_blue_diamond: 

Now lets finish up this function.  Grab the execution pin from **Set Starting Position** and connect it to the **Set | Starting Position** node.  Then take the vector output **Get Actor Location | Return Value** to the **Set | Starting Position** input pin. 

Please note that white triangles determines the execution order of the nodes (it is not where it is positioned on the graph).  The colored dots is data coming out (right hand side) and into (left hand side) nodes.  Each color represents a different data type.  In this case yellow represents a vector.

![create startingPosition variable](images/finishUpFunction.png)

![](../images/line2.png)

##### `Step 14.`\|`UE5LD`| :large_blue_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:  :small_blue_diamond: 

Go back to the leven and delete the static mesh of the moving platform.  Replace it with **Blueprints | BP_MovingPlatform**.  It looks the same but in this case it has extra logic. Move it into the **Moving Platform** folder in the **World Outliner**. Ntotice the **Starting Position** variable gets the current **World Position** of the platform. 

![replace mesh with bp](images/replaceWithBlueprint.png)

![](../images/line2.png)

##### `Step 15.`\|`UE5LD`| :large_blue_diamond: :small_orange_diamond: 

Now go into the game and adjust the platform to an appropriate starting position and press the **Set Starting Position** button that is exposed in the editor. Remember the only way you can get access to this function in the **World Outliner** is to turn **Call in Editor** to true in the function as we did above.

https://github.com/maubanel/UE5-Level-Design/assets/5504953/f55d7447-a826-4c5f-83d0-2d924f2f4ec0



![](../images/line2.png)

##### `Step 16.`\|`UE5LD`| :large_blue_diamond: :small_orange_diamond:   :small_blue_diamond: 

Duplicate the **Starting Position** variable and call it `EndingPosition` and change the tooltip to `Ending location of the platform`. Otherwise everything else can stay the same.  This will store the ending location so the platform will move between the starting and ending position we set.

![duplicate starting position ot create end position](images/endingPos.png)

![](../images/line2.png)

##### `Step 17.`\|`UE5LD`| :large_blue_diamond: :small_orange_diamond: :small_blue_diamond: :small_blue_diamond:

Now we need a function to set the ending position.  Right click on **SetStartingPosition** function and select **Duplicate**.  Call this new function `SetEndingPosition`.  Now we need to right click on the **Set | Starting Position** and select `Replace variable 'Staring Position' with ... > | EndingPosition`. 

![duplicate function to set ending position](images/dupeFunction.png)

![](../images/line2.png)

##### `Step 18.`\|`UE5LD`| :large_blue_diamond: :small_orange_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

Change the **Description** to `Set the ending position of the platform`. 

![change description of set end function](images/changeDescription.png)


![](../images/line2.png)

##### `Step 19.`\|`UE5LD`| :large_blue_diamond: :small_orange_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond: :small_blue_diamond:

Now you can go back to the game and move the platform to the ending location.  Press the **Set End Location** button and see the **EndLocation** variable update with the new **World Position**.

https://github.com/maubanel/UE5-Level-Design/assets/5504953/d72065b1-f4f7-4f22-843b-fb52c4c0c132

<!-- <img src="https://via.placeholder.com/1000x100/45D7CA/000000/?text=COMPLETE!"> -->
![next up next tile](images/banner.png)


| [previous](../long-jump/README.md#user-content-long-jump)| [home](../README.md#user-content-ue4-intro-to-level-design) | [next](../moving-platform-ii/README.md#user-content-moving-platform-ii)|
|---|---|---|
