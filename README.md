# "DAVIS-Ag" Dataset

(This page is under update)

This repository is for the official release of the "DAVIS-Ag" dataset, introduced in: 

> *"DAVIS-Ag: A Synthetic Plant Dataset for Developing Domain-Inspired Active Vision in Agricultural Robots"*. Taeyeong Choi, Dario Guevara, Grisha Bandodkar, Zifei Cheng, Chonghan Wang, Brian N. Bailey, Mason Earles, and Xin Liu. [\[arXiv:2303.05764\]](https://arxiv.org/pdf/2303.05764.pdf). 

For research in active vision in Agricultural scenarios, DAVIS-Ag presents >502K RGB images with useful labels from  632 realistically synthesized plant environments. In particular, you can simulate an embodied agent that can move without any complicated components (e.g., gaming engines, ROS, etc.) because viewpoints for imaging were sampled from densely distributed locations while each viewpoint is also linked with others if *reachable* by an execution of action. 

Pixel-wise segmentations and bounding boxes of fruits are available with unique "instance" ID's for studies on instance-level fruit detection/coverage. Global poses of cameras are also provided for development of vision-based navigation/localization. More details are described below. 

# Download

The link to download the full dataset will be offered very soon. In the meantime, feel free to explore <a href="https://ucdavis365-my.sharepoint.com/:f:/g/personal/taechoi_ucdavis_edu/Eoc5VOEXhqhHsP3jU9PzqS4BQQZ9hIs5zJmRuVhJwLTEsw?e=lMNmP0" target="_blank">example data</a>.

<!-- # Generation Framework  -->

# Directory Structure

Once you have downloaded DAVIS-Ag, you could find its structure of directory as below: 
```
"Scenario-Plant_Type"
 └── "Scene_#" 
     ├── "annotations.json"  
     └── "images" 
           ├── "Image_#.jpeg"
           └── "Image_#_seg.png"
```

For example, under `Single-Tomato`, you could see: 

```
Single-Tomato
 ├── 000 
 ├── 001 
 ├── 002 
     ├── annotations.json 
     └── images 
          ├── 0001.jpeg
          ├── 0001_seg.png
          ├── 0002.jpeg
          ├── 0002_seg.png
           ...
          ├── 0347.jpeg
          └── 0347_seg.png 
 ...
 ├── 135 
 └── 136  
```

Each `*.jpeg` is a RGB image of 1280x720 taken from a particular viewpoint, and `*_seg.png` is a image file of the same size that shows the corresponding pixel-wise segmentation of fruits. 
`annotations.json` contains all other useful labels, explained [Labels](#labels) section below.


# Scene Environments  

Three types of plants are simulated: `Strawberry`, `Tomato`, and `Goblet Vine`, and for each type, two different scenarios are considered depending on the size of the scene. 

- *Single-plant (SP)*: One single plant is positioned at the central location of the scene; Camera views from any positions are designed to always aim at the plant; Three different altitudes of view are simulated; Six actions are considered: *Forward, Backward, Left, Right, Up*, and *Down*.

- *Multi-plant (MP)*: Three plants in a row are present in each tomato or vine scene while five in a row in a strawberry scene; Two levels of height of view are simulated; Eight actions are executable: *Forward, Backward, Left, Right, Up, Down, Rotate_Clockwise,* and *Rotate_Counterclockwise*.

In total, 502,542 RGB images and associated labels are available. More specific stats for both scenarios are shown in the tables below.

| SP  | Total | Strawberry  |  Tomato | Goblet Vine | 
|:-:|---|---|---|:-:|
| # of Scenes  | 398 | 86  | 130  | 182  |
| # of RGB Images  | 133,086  | 24,510  | 45,240  | 63,336  | 

| MP  | Total | Strawberry  |  Tomato | Goblet Vine | 
|:-:|---|---|---|:-:|
| # of Scenes  | 234 | 77  | 113  | 44  |
| # of RGB Images  | 369,456  | 86,856  | 203,400  | 79,200  | 


<!-- spatial distribution / variations in position / variations in phenotypes  -->

# Labels & File Format

Each RGB image (`*.jpeg`) is provided with the following labels: 

1. Pixel-wise instance segmentation of fruits (`*._seg.png`)

2. Bounding boxes of fruits

3. Global pose of viewpoint

4. Action pointers

where 2–4 are all provided in `annotations.json`. 

 | RGB of Goblet Vine | Seg of Goblet Vine |
|:-:|:-:|
|![rgb_vine](figures/single_vine_rgb.png)| ![seg_vine](figures/single_vine_seg.png)|

| Bounding Boxes of Strawberries  | Bounding Boxes of Tomatoes  |
|:-:|:-:|
|![rgb_vine](figures/single_strawberry_bb.png)| ![seg_vine](figures/single_tomato_bb.png)|

In particular, DAVIS-Ag offers 1 and 2 with unique instance ID's of fruits in the scene. For instance, each pixel in `*_seg.png` can represent a unique instance ID of fruit in the scene. Pixels that are not of any fruit are set to 255. 

In addition, inspired by <a href="https://www.cs.unc.edu/~ammirato/active_vision_dataset_website/index.html" target="_blank">Active Vision Dataset</a>, `annotations.json` is designed to show bounding boxes and other labels:

```
{
    "image_name":{
      "bounding_boxes":[
          [xmin ymin width height instance_id 0],
          [xmin ymin width height instance_id 0],
          ...,
      ],
      "pose": [x, y, z, yaw, pitch],
      "forward":"another_image_name",
      "backward":"another_image_name",
      "left":"another_image_name",
      "right":"another_image_name",
      "up":"another_image_name",
      "down":"another_image_name",
      "rotate_ccw":"another_image_name",
      "rotate_cw":"another_image_name"

  },
  "next_image_name":{ ...
  
}
```

Forth entry (`instance_id`) in a bounding box can be used to track a particular instance of fruit. Also, `pose` represents the pose of camera that was used to take the image in the global coordinate system. 

Furthermore, each possible action is linked with another image file to simulate the action of embodied agent. If the action leads to a position out of the grid or too close to a plant, "" is given. 


# Generation Pipeline 

Two major software components have been fully utilized to produce DAVIS-Ag: 

1. <a href="https://baileylab.ucdavis.edu/software/helios/" target="_blank">Helios</a>
2.  <a href="https://github.com/Project-AgML/AgML" target="_blank">AgML</a>

which are both actively developed by research groups based in the University of California, Davis. 

More specifically, several plugins in Helios were used to synthesize realistic visual data of plant with useful annotations whereas AgML worked as an interface for Python scripts to freely access those plugins for particular purposes for generation of DAVIS-Ag. 

For those who are interested in more technical details, reading the [paper](#davis-ag-dataset) on the top is strongly recommended.


# Supplementary Video

https://youtu.be/CIXA1qgl6JM 

# Contact

If you have any questions, please feel free to send an email to: taechoi@ucdavis.edu.
