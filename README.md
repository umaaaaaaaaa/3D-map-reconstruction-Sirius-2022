# 3D-map-reconstruction-Sirius-2022
Neural network reconstruction of 3D semantic maps, AIRI x Sirius 2022

## The Task of the project

The goal is a 3D reconstruction of the bottom surface, with which we can then calculate the volume of the biotope (in our case crabs). At the entrance, we receive a monocular video extracted from online recordings of the seabed from youtube. As a result, we get a three-dimensional map in the form of a mesh with detected crabs and the volume of crabs found in the video

The project is relevant because it is necessary to automate detailed underwater research, which is mandatory in the Russian Federation. The areas of application can be:
- Exploration inspection work on water bodies
- Environmental monitoring during construction on the continental shelf
- Monitoring of fishing sites

## Our pipeline

 Our pipeline includes the steps, described on the picture below.
 ![pipeline](https://user-images.githubusercontent.com/88504487/183307573-62930939-ee17-4393-842c-eb60dd6cfce9.jpg)
 
 The following figure contains a detailed description of the components of the [Hierarchical-Localization network](https://github.com/cvg/Hierarchical-Localization/)  and the [Poisson method](https://github.com/mfdeveloper/surface_reconstruction_python#usage) implemented in open3d. As a result, we get the restored surface of the seabed from a series of frames.
 ![mesh_reconstruction](https://user-images.githubusercontent.com/88504487/187232520-7d0a51f0-0ad9-4371-b3b7-b51fa8439484.jpg)
## Results
As an input data we have [this video](https://www.youtube.com/watch?v=Mq8LFUyvBrM&t=41s) from youtube. 
Next, we get a point cloud with approximate camera positions. And using the Poisson method, we get a surface. We can pull the original image onto a surface where we can see crabs.
![example](https://user-images.githubusercontent.com/88504487/187242244-0e56ba72-bfca-41c6-981e-6039d62d7d6f.png)

The following is another example obtained from a video recording using our approach.

![example2](https://user-images.githubusercontent.com/88504487/187243402-420db25c-e426-44c3-af44-61f0591001ba.png)

## Objects segmentation
In this part of the solution, we segment the images to find crabs on them, and then correlate the objects in the image and on the 3d mesh using the built-in localization in hloc.
![segmentation](https://user-images.githubusercontent.com/88504487/187244774-3daa506f-4a5b-44ab-9a3d-8ec9a8f63982.png)

## Other tested methods
We also tried [neuralblox](https://github.com/ethz-asl/neuralblox), which of the depth maps and camera positions can restore the surface, however, on our data, this method did not prove itself very well. Perhaps more static images of the same place are needed for a good result.

![neuralblox](https://user-images.githubusercontent.com/88504487/187246041-e5dd8f92-39ef-486b-84ad-2945a6bfc621.jpg)

Another tried method is [VDBFusion](https://github.com/PRBonn/vdbfusion). This neural network, under certain parameters, gave good approximations of the surface, but the surface has noise, so we preferred a more stable classical version of surface reconstruction.
![vdbfusion](https://user-images.githubusercontent.com/88504487/187246086-b3d2322c-5b22-4017-bdbc-5bd2ffd1b6b0.jpg)

 ## What's next?
Despite the fact that we tried various non-classical methods of solving our problem, in conditions of limited time, we still could not implement all the ideas.
 
One of the unrealized ideas was to compare areas with 2D images from a video with 3D mesh to identify crabs using the ray tracing method. To find a specific 3D point on the mesh, we should find the intersections of a ray from camera center, through the 2d point on the image plane and the mesh.This can be implemented using the [trimesh](https://github.com/mikedh/trimesh) library. The example code can be viewed [here](https://github.com/mikedh/trimesh/blob/master/examples/raytrace.py).

Also, we have not tried many other approaches to restoring misha from a point cloud, for example, the following approaches:
- [OpenMVC](https://github.com/cdcseacave/openMVS)
- [PackNet](https://github.com/tri-ml/packnet-sfm)
- [Vis2mesh](https://github.com/GDAOSU/vis2mesh)

It would also be interesting to explore how the newly released [MobileNerf](https://mobile-nerf.github.io/) can be applied to the task.


 
