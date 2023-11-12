# Giant Particle - Inspector Graph Pro <!-- omit in toc -->
The Inspector Graph Pro is a tool to better visualize, understand and manipulate objects in a reference hierarchy. It includes all the features from the original [Inspector Graph](https://github.com/giantparticlegames/InspectorGraph) plus extra functionality.

![Window Sample](.imgs/WindowSample.png)

## Index <!-- omit in toc -->
- [Pro Features](#pro-features)
- [Change log](#change-log)
- [Feature Details](#feature-details)
  - [Addressables References](#addressables-references)
  - [Scene Object](#scene-object)
  - [Automatic objects inspection based on selection](#automatic-objects-inspection-based-on-selection)
  - [Scroll Wheel Zoom](#scroll-wheel-zoom)
  - [New Inspection Modes](#new-inspection-modes)
    - [Asset References To Object Mode](#asset-references-to-object-mode)
      - [How it works?](#how-it-works)
      - [How is it displayed?](#how-is-it-displayed)
    - [Scene References To Object Mode](#scene-references-to-object-mode)
      - [How it works?](#how-it-works-1)
      - [How is it displayed?](#how-is-it-displayed-1)

## Pro Features
* Support for Addressables References
* Support to inspect Scene objects
* Automatically inspect objects based on selection in Project or Hierarchy panel
  * Lock inspected object to avoid accidental changes in graph
* Zoom in and out using [Alt on PC / Option on Mac] + Scroll Wheel
* Extra Inspection modes
  * Inspect references from Assets in Project to the Target asset
  * Inspect references from Active Loaded Scene to the Target asset
* Cache Asset Database to quickly scan project assets

## Change log
Take a look at the latest changes [here](CHANGELOG.md).

## Feature Details
> **Important**</br>
> For some of these features to work correctly, your assets must be serialized as Text. The serialization mode can be changed via `Project Settings`
> ![](.imgs/project_settings_serialization.png)

### Addressables References
Inspector Graph Pro can recognize [Unity Addressables](https://docs.unity3d.com/Packages/com.unity.addressables@2.0/manual/index.html) references. These references will be displayed in the Reference Graph with a distinct color (Magenta by default) that can be configured via [Inspector Graph Project Settings](https://github.com/giantparticlegames/InspectorGraph/blob/main/README.md#project-settings).

![Addressable Reference](.imgs/Addressable_Reference.png)

### Scene Object
Inspector Graph Pro supports the inspection of Scene objects. When selecting a Scene, the graph will display all references to external assets outside the scene, embedded data in the scene will not be displayed (Example: GameObjects that are not Prefab Instances)

![Scene Object](.imgs/Scene_Object.png)

> ℹ️ Note: This feature requires Text Asset Serialization

### Automatic objects inspection based on selection
Inspector Graph Pro can automatically change the inspected object based on the selected objects from the Hierarchy or Project panels. To prevent unintended changes in the graph visualization, a convenient Lock button is placed next to the active Object selection to prevent it from changing when selecting objects.

> ℹ️ Note: Inspector Graph can only inspect one object at a time, multiple selections will have no effect on the graph.

| Lock Selection | Unlocked Selection |
| -- | -- |
| ![Locked Selection](.imgs/locked_selection.png) | ![Unlocked Selection](.imgs/unlocked_selection.png) |

| Project Selection |
|--|
| ![Project Selection](.imgs/project_selection.png) |

| Hierarchy Selection |
|--|
| ![hierarchy Object](.imgs/hierarchy_selection.png) |

### Scroll Wheel Zoom
In addition to regular zoom control, Inspector Graph Pro provides a faster and more accurate way to Zoom in and out the graph using the Mouse Scroll Wheel.</br>
Simply Press and Hold the `Alt` key on PC or `Option` key on Mac and move the Mouse Scroll Wheel **Up to Zoom In** or **Down to Zoom out**. The center position of the zoom will be located where the mouse position is on the graph.

### New Inspection Modes
Inspector Graph Pro provides extra inspection modes that can be selected via `View > Inspection Modes` under the Inspector Graph Window.

![Inspection Modes](.imgs/inspection_modes.png)

At the moment, there are two extra inspection modes, `Asset References To Object` and `Scene References To Object`. One is focused on references from other assets in the project and the other is focused on references from the active loaded scene.

#### Asset References To Object Mode
This mode will display all references from Other Assets in the project to the active object.

> ℹ️ Note: This feature requires Text Asset Serialization

##### How it works?
Inspector Graph will scan all assets in the Project extracting all recognizable references. This process may take some time the first time it runs depending on the size of your project, the results will be cached and subsequent runs will execute much faster.

The scan runs in the background and it will not block the usage of Unity, keep in mind to avoid changing references of assets while this is happening to avoid inaccuracies. When Inspector Graph is scanning, it will display a progress bar at the bottom right corner of the Inspector Graph Window.

![Scanning Progress Bar](.imgs/scanning_progress_bar.png)

##### How is it displayed?
The graph will change direction and all the assets found that contain a reference to the active object will display first and only the references to the Active Object will be displayed to avoid unnecessary noise.

![Assets Referencing Target Example](.imgs/asset_references_example.png)

#### Scene References To Object Mode
This inspection mode is intended to provide a better understanding of the usage of a particular asset on a given Scene.

##### How it works?
In order to detect the references to the active Object from a particular scene, the scene must be loaded and active. Once that is done, select this mode to scan for references or refresh the view. Inspector Graph will scan all the objects in the active loaded scene for references to the active object.

##### How is it displayed?
Similarly to `Asset References To Object` mode, the graph will change direction and all the scene objects that are referencing the active object will be displayed first and only references to the Active Object will be displayed to avoid unnecessary noise. Also, instead of displaying GameObjects as a whole, only the scripts with references will be displayed unless is a PrefabInstance.

![Assets Referencing Target Example](.imgs/scene_references_example.png)
