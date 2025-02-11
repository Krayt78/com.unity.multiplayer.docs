---
id: helloworldintro
title: Your First Networked Game "Hello World"
---
This "Hello World" guide walks you through creating a project, installing the MLAPI package, and creating the basic components for your first networked game.

## Create a new project in Unity

1. Open the Unity Hub.
1. Click New. 
1. Select type ‘3D’
1. Rename the project "Hello World".
1. Select the location to save the project.

:::important
This tutorial requires an MLAPI-supported version of Unity (2019.4+).
:::

 ![Open Unity create new project](/img/openunity.gif)

## Import MLAPI Package via URL

See the [Install MLAPI](../migration/installation.md) guide to install the MLAPI package.

## Create the Basic Components

1. Right click in the Hierarchy tab of the Main Unity Window.
1. Select **Create Empty**.
1. Rename the GameObject **NetworkManager**.
   
    ![create gameobject](/img/creategameobject.gif) 
  :::tip
  We renamed the GameObject because:
    * It makes it  easier to refer to later.
    * There is one and only one **NetworkManager**, this is the object that contains the  `NetworkManager` component.
  :::

  You have now created a new GameObject called **NetworkManager**.

1. Select **NetworkManager**.
1. Click **Add Component** in the Inspector Tab.
1. Select **MLAPI** from the list shown.
1. Select `NetworkManager` Component from the list displayed.
1. Inside the `NetworkManager` component tab, locate the  `NetworkTransport` field. 
1. Click "Select Transport".
1. Select `UnetTransport`.

  ![selecttransaportani](/img/selecting-transport.gif)

1. Create 3D Object->Capsule (name it **Player**). 
1. Add a `NetworkObject` component.
1. Click the Assets folder.
1. Create a new Folder and call it **Prefabs**.
1. Make **Player** a prefab by dragging it to **Prefabs** folder you just created.

  ![createplayer prefab](/img/createprefab.gif)

1. Delete **Player** from scene.

  :::tip
  We remove **Player**, because we will be using the network library to spawn the player. The library cannot track objects that start in the scene.
  :::

1. Add Player prefab to `NetworkPrefabs` list inside of `NetworkManager`.
1. Select **Default Player Prefab**.

  ![addingdefaultprefab](/img/default-player-prefab.gif)

  :::tip
  When you select the **Default Player Prefab** , you are telling the library that when a client connect to the game, automatically spawn this prefab as the character for the connecting client. If you do not have the default selected for any prefab the game will crash on client connect.
  :::
  :::note
   You may see the following error reported `There is no NetworkPrefab Marked as a PlayerPrefab`. Once you have completed the above steps you can clear the error.
  :::

1. Create a 3D Object->Plane, centered at (0,0,0).
1. Click **Play**.
1. Click **Start Host** under **NetworkManager**. 

  ![firstnetworkgame](/img/firstnetworkgame.gif)

:::note Congrats!
Congratulations you have created a networked game. It is not a very flashy game but it is a networked game nonetheless. For the next steps in your journey see [Building on "Hello World"](helloworldparttwo.md)
:::
