# "DAVIS-Ag" Dataset

(This page is under update)

This repository is for the official release of the DAVIS-Ag dataset, introduced in: 

> *"DAVIS-Ag: A Synthetic Plant Dataset for Developing Domain-Inspired Active Vision in Agricultural Robots"*. Taeyeong Choi, Dario Guevara, Grisha Bandodkar, Zifei Cheng, Chonghan Wang, Brian N. Bailey, Mason Earles, and Xin Liu. [\[arXiv:2303.05764\]](https://arxiv.org/pdf/2303.05764.pdf). 

For research in active vision in Agricultural scenarios, DAVIS-Ag presents >502K RGB images with useful annotations from  632 realistically synthesized plant environments. In particular, to simulate an embodied agent that can move, viewpoints for images were selected from densely distributed locations while each image is also linked with others that are *reachable* by an execution of actions. 

Moreover, pixel-wise "instance" segmentations and bounding boxes of fruits are available for studies on fruit detection/coverage. Global poses of cameras are also provided for development of vision-based navigation/localization. 

More details follow below. 

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
`annotations.json` contains all other labels, described [Labels](#labels) section below.


# Scene Environments  

Three types of plants are simulated: Strawberry, Tomato, and Goblet Vine, and for each type, two different scenarios are considered depending on the size of the scene in simulation. 

- *Single-plant*: One single plant is positioned at the central location of the scene; Camera views from any positions are designed to always aim at the plant; Three different heights of view are simulated; Six actions are considered: *Forward, Backward, Left, Right, Up*, and *Down*.

- *Multi-plant*: Three plants in a row are present in each tomato or vine case while five in a row in a strawberry scene; Two levels of height of view are simulated; Eight actions are executable: *Forward, Backward, Left, Right, Up, Down, Rotate Clockwise,* and *Rotate Counterclockwise*.


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



# Supplementary Video

https://youtu.be/CIXA1qgl6JM 

# Contact

If you have any questions, please feel free to send an email to: taechoi@ucdavis.edu.
