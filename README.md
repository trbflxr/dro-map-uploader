Instructions for uploading tracks to workshop from a mod project

1. Preparation of the route loading project
2. Import a 3d model of the route into the project
3. Adding the main components
 - Assignment of surface collisions
 - Assignment of the point of appearance on the map
 - Assignment of ambient sounds
 - Adding a minimap
4. Unloading the route in the workshop

1) Preparation of the route loading project
First you need to pump out the project itself. It is available at the link https://github.com/CarXTechnologies/dro-map-uploader Connect your Github account. You can download a zip archive and unpack it anywhere in the file system
(Code → Download ZIP)
Next, to open the project, you need to install the Unity editor, you need the Unity version 2020.3.25, download link (only for 64x bit systems)
https://download.unity3d.com/download_unity/9b9180224418/Windows64EditorInstaller/UnitySetup64-2020.3.25f1.exe The
next step is to launch Unity, select the File → Open Project menu and select the folder containing the unpacked project (there should be Assets, Packages, etc. folders in this folder)
The project is ready, you can proceed to the next item

2) Import a 3d model of the route into the project
In the Assets/MapResources/ folder, create a folder with the working name of the map.
In the created folder, you need to create a scene through the Assets → Create → menu Scene.
Next, you need to download .fbx/.obj/.dae (Collada) from programs such as Blender/Maya/Autodesk 3ds max. To do this, use Drag&Drop you need to move the 3d model to the Assets/MapResources/%your_folder% folder/
If the materials are not configured in the models, then create the material via the Assets → Create → Material menu and configure (see example below)
Open the created scene (item 2) and create a scene object (GameObject) by transferring the 3d model to the scene.
For the created GameObject, add the necessary components (section 3).
To create a reusable object (Prefab), create the Assets/MapResources/%your_folder%/ Prefabs folder.
Right-click on the object in the scene and select the Prefab → Unpack Comletely menu.
Next, move the GameObject to the created Prefabs folder from the scene. Thus, it becomes possible to reuse the object the required number of times.
3) Adding the main components
The project supports several types of components that are transferred to the game. The main ones are:
the point of appearance of the car on the map, the sounds of the environment, the physical materials of the surfaces

These components are assigned via the GameMarkerData auxiliary component.
To add a component to a scene object (GameObject) or an object in a project (Prefab) in the Inspector window, click the Add Component button and enter the name GameMarkerData.
It is also possible to add a mini-map.

a. Assignment of surface collisions
For the route object representing the surface, select the type of the GameMarkerData Road component, and in the dropdown, select the required type of material to be used in the game when hitting this surface.

Note that any GameObject/Prefab with a collision must also be with some Collider type component (Box/Sphere/Capsule/Mesh Collider). This condition is necessary for the correctness of collisions.

b. Assignment of the point of appearance on the map
To assign a point of appearance on the map, select the menu item GameObect → Create Empty (or Ctrl+Shift+N). In the Transform component, set the coordinates of the point that is most suitable for the appearance of the car in the game. Add the GameMarkerData component, and select the SpawnPoint type

c. Assignment of ambient sounds
To assign a point of appearance on the map, select the menu item GameObect → Create Empty (or Ctrl+Shift+N). Add the GameMarkerData component, and select the Ambient type. Next, in the dropdown, select the sound type that best suits the situation on the map.

When adding an Ambient marker, you can use the DrawZoneBehaviour component - this is an auxiliary component that draws the area of the component. For example, for an Ambient marker, this component will show the zone in which the assigned sounds will be heard.
If another auxiliary script is needed, then you can write it yourself and add your own along the path Assets/Resources/MapSkipComponent

d. Adding a minimap
It is also possible to add an optional minimap object. To do this, create an empty object on the scene (see above) and add the Minimap component. Next, you need to select the Minimap layer. In the Textures → Element 0 field, you need to assign at least one texture - MainTexture

4) Unloading the route in the workshop
To upload, you first need to create a map config in the maps folder
Next, you need to configure the config. To do this, you need:
- *specify the name of the working scene.
- *enter the name of the card to be displayed in the workshop
- enter a description of the map to be displayed in the workshop
- *assign Icon - a map icon that will be displayed in the list of workshop maps in the game itself
- *assign a Large icon - a preview of the map that will be displayed in the workshop and when entering the map in the game itself
- Item Workshop Id - the ID of the card received when uploaded to the workshop (assigned automatically after publication)
- Upload Steam Description - if enabled, the description on the workshop page will definitely be updated
- Upload Steam Name - if enabled, the name of the card on the page in the workshop will definitely be updated
- Upload Steam Preview - if enabled, the map icon on the workshop page will definitely be updated
(*) - required field

To install the scene as an assembly in Steam, select the MapMetaConfig that was created before in Resources/MapManagerConfig
When everything is ready, it's time to export to steam, to do this, open steam, after there are
several items to select the build

Create - Just assemble the map if there are no errors. Then the map is made correctly. It also creates an intermediate result in Asset/{MapName}

Create and publication - Collects the map and sends it to the workshop, if the map is assembled and successfully passes the publication stage, there will be no errors in the console

Update exist publication - updates an existing publication to which you have access, the id of the last publication is specified in the Item Workshop Id field

If the card is configured incorrectly, then an error will be displayed during unloading, the reasons for which will need to be resolved independently.

After completing these points, the map will be published in steam workshop. Initially, the visibility of the downloaded map will be as “Private". So, you can test the created map in the game, and it will be visible only to the author. To do this, go to the Workshop → Workshop Tracks menu in the game. You can change the visibility to “For everyone" on the map page in the workshop.

Important! At the moment, the “Friends Only" visibility is not working correctly. This is due to a problem on the side of the external library through which we work with the steam api. We will deal with this problem in subsequent releases.
