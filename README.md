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

 ## What's next?
Despite the fact that we tried various non-classical methods of solving our problem, in conditions of limited time, we still could not implement all the ideas.
 
One of the unrealized ideas was to compare areas with 2D images from a video with 3D mesh to identify crabs using the ray tracing method. To find a specific 3D point on the mesh, we should find the intersections of a ray from camera center, through the 2d point on the image plane and the mesh.This can be implemented using the [trimesh](https://github.com/mikedh/trimesh) library. The example code can be viewed [here](https://github.com/mikedh/trimesh/blob/master/examples/raytrace.py).

Also, we have not tried many other approaches to restoring misha from a point cloud, for example, the following approaches:
- [OpenMVC](https://github.com/cdcseacave/openMVS)
- [PackNet](https://github.com/tri-ml/packnet-sfm)
- [Vis2mesh](https://github.com/GDAOSU/vis2mesh)

It would also be interesting to explore how the newly released [MobileNerf](https://mobile-nerf.github.io/) can be applied to the task.


<p>
<iframe width="560" height="315" src="https://www.youtube.com/embed/Mq8LFUyvBrM" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</p>
