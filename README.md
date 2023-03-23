# "DAVIS-Ag" Dataset

(This page is under update)

This repository is for the official release of the DAVIS-Ag dataset, introduced in: 

*"DAVIS-Ag: A Synthetic Plant Dataset for Developing Domain-Inspired Active Vision in Agricultural Robots"*. Taeyeong Choi, Dario Guevara, Grisha Bandodkar, Zifei Cheng, Chonghan Wang, Brian N. Bailey, Mason Earles, and Xin Liu. [\[arXiv:2303.05764\]](https://arxiv.org/pdf/2303.05764.pdf). 

For research in active vision in Agricultural scenarios, DAVIS-Ag presents >502K RGB images with useful annotations from  632 realistically synthesized plant environments. More details follow. 

# Download Link

Link to download the full dataset will be offered very soon. In the meantime, feel free to explore <a href="https://ucdavis365-my.sharepoint.com/:f:/g/personal/taechoi_ucdavis_edu/Eoc5VOEXhqhHsP3jU9PzqS4BQQZ9hIs5zJmRuVhJwLTEsw?e=lMNmP0" target="_blank">example data</a>.


<!-- # Generation Framework  -->

# Scenes  

Three types of plants are simulated: Strawberry, Tomato, and Goblet Vine. 



In addition, two different scenarios are considered depending on the size of the scene in simulation. 

- *Single-plant*: One single plant is positioned at the central location of the scene; Camera views from any positions are designed to always aim at the plant; Three different heights of view are simulated; Six actions are considered: *Forward, Backward, Left, Right, Up*, and *Down*.

- *Multi-plant*: Three plants in a row are present in each tomato or vine case while five in a row in a strawberry scene; Two different heights of view are simulated; Eight actions are executable: *Forward, Backward, Left, Right, Up, Down, Rotate Clockwise,* and *Rotate Counterclockwise*.



# Labels


To be specific, each RGB image is provided with the following labels: 

1. Pixel-wise instance segmentation of fruits
 
 | RGB  | Seg  |
|:-:|:-:|
|![rgb_vine](figures/single_vine_rgb.png)| ![seg_vine](figures/single_vine_seg.png)|

2. Bounding boxes of fruits 

| Strawberries  | Tomatoes  |
|:-:|:-:|
|![rgb_vine](figures/single_strawberry_bb.png)| ![seg_vine](figures/single_tomato_bb.png)|

# Supplementary Video

https://youtu.be/CIXA1qgl6JM 

# Contact

If you have any questions, please feel free to send an email to: taechoi@ucdavis.edu.
