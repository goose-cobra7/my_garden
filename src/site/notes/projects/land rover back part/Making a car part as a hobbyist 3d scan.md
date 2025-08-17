---
{"dg-publish":true,"permalink":"/projects/land rover back part/Making a car part as a hobbyist 3d scan/"}
---

#projects 
*I'm taking this project also as opportunity to learn more and expend my knowledge worst case scenario we get cool models, documentation and plus we learn more cool stuff*

> [!NOTE] disclaimer
> as it stand right now. the project is abandon.
> reasons being: tech problem, the project it self goes into a holt because even if i could bring a final 3d model, the changes of it being i level fitting for car part is very low.
> as a result I'm getting some done and finishing it. but no, the project is not done. but all models and doc' will be release.

# the plan
the plan is to scan the one part we have scan the area of assembly on the car, using softer refine it and make it to 3d model, send it either to 3d print or to laser cutting and welding
3d printing is easier but also cheaper and look way worst then 3d metal part by laser: this is way we using the 3d model to make 2 parts; one for 3d print and one for metal fabrication
# apps in use for project
3d modeling - [blender](https://www.blender.org/download)
for scan review and pipelining 

3d scanning - [meshroom](https://alicevision.org/#meshroom)
free, opensource software for 3d scanning using camera
https://github.com/alicevision/Meshroom?tab=readme-ov-file

3d printing - 
cad - [onshape](https://www.onshape.com/en)
easy, free, cad software for basic work and planing
# 3d scanning plan
i know that the [3d scanning](https://en.wikipedia.org/wiki/3D_scanning) we use here is not perfect definitely not for the cad work we do, but it will allow us to make the progress way fester, focusing and the difficult part like modeling holes and precise shape and aligning the models.
plus i might the chance to 3d scan more part.
creating library of parts.
# photo file for scanner
so we done with the first photoshoot session we got something off 150-200 pics 
![meshroom pic1.png|716](/img/user/projects/%F0%9F%96%BC%EF%B8%8Fpic/meshroom%20pic1.png)
we started by just throwing it all to the software and letting at run the first stages, if more photos need then we can just grab the camera and go take more. 
the camera i use [nikon coolpix p100](https://www.photoreview.com.au/reviews/advanced-compact-cameras/fixed-lens/nikon-coolpix-p100/)
but you can use any camera or phone
![nikon p100.jpg|297](/img/user/projects/%F0%9F%96%BC%EF%B8%8Fpic/nikon%20p100.jpg)
we run the software until the [Structure from Motion stage](https://alicevision.org/#photogrammetry/sfm)
## GPU meshroom
we run into problems with MeshRoom and [cuda cores](https://en.wikipedia.org/wiki/CUDA) (Nvidia GPU). mesh room said to be using gpu to optimize part of the process (some task are better done with GPU). but when we run the software we found that only the cpu run. we dug into it.
solution: GPU is part of the pc that take jobs that need processing, in long story short, if you don't the gpu you want him to join the fight is just sitting there.
so we went to the Nvidia control panel and change it to include MeshRoom in the softwares list of the gpu
## fixing needed
![meshroom scan point zoom in missing area.webp|350](/img/user/projects/%F0%9F%96%BC%EF%B8%8Fpic/meshroom%20scan%20point%20zoom%20in%20missing%20area.webp)
as you can see even though we took 109 pic we missed a spot, this calls for taking the camera and going to shoot even more in the missing area.
![mesh room pipeline of work.webp](/img/user/projects/%F0%9F%96%BC%EF%B8%8Fpic/mesh%20room%20pipeline%20of%20work.webp)
the process is easy as just putting more pic into the project and running the process again. the only diffrent now you have 2 branch the old computation and the new combining.
so the top line is the old and the bottom one is the new pipeline.
and thx for the GPU fix we done, the old branch and the fix only being 60 pics the process run way faster.
by the look of things because of the dark area of the shadow i couldn't get the fix to fill the missing hole. but we might try to fix it in the postprocess. it should be all good cause its not a complex part to model and fix.
![meshroom dot scan match points.webp|447](/img/user/projects/%F0%9F%96%BC%EF%B8%8Fpic/meshroom%20dot%20scan%20match%20points.webp)
the green square is the area of the problem. the shadows was so dark compere to the other parts and picture that the software could not find matching features between the pictures. 
the red square is floating points left from mismatching of the feature matching. i hope the cleanup will fix this and would not create artifact.
# final scanned model
![mesh room landrover back part left scan mash.webp|389](/img/user/projects/%F0%9F%96%BC%EF%B8%8Fpic/mesh%20room%20landrover%20back%20part%20left%20scan%20mash.webp) 
*the 3D scan in the MeshRoom. the more dark the more tringles and vertices and better accuracy*
the black/gray area is the mash having a lot of detail, a lot of tringles. which is good.
now e do the same for the other side of the car the side that missing the part. 
then we match the parts clean them and go for the next step.
after having the 2 parts in post process in right size and and good optimization, we are pass the hard part of the project and its smooth ride.
![landrover back left part project meshroom blender.webp|375](/img/user/projects/%F0%9F%96%BC%EF%B8%8Fpic/landrover%20back%20left%20part%20project%20meshroom%20blender.webp) 
*the 3d scan of the left side in Blender*
the same part in blender. cant believe how easy it is. just drag and drop.
## second model
the second model was easy as the first, with same amount of problems. we needed to take some more photos. but it worked like a charm the most important think is to see if the holes as bean detected by the software
**![landrover in blender.webp](/img/user/projects/%F0%9F%96%BC%EF%B8%8Fpic/landrover%20in%20blender.webp)**
2 off the models in blender with texturing
## fixing the model
the model is out with a lot of holes and tears, and needing fix. 
i researched a little bit and found meshleb
free software to do exactly this

so in meshlab i clean and fix what i can throw it back to blender for more fix
ill tell you all the steps later

then upload it to onshape
onshape doesn't like the obj type and really doesn't like the scans, causing me more pain

after uploading the model with better topology, its time to make some cad.
## the process (and pain) for right topology
*i will say that for the next project what we going to do is just better and longer scanning.
this will solve a lot of problems like holes and large imperfections*


# cad model
## what we need to make
for a start we need to align  the models with right accuracy and measurement
one model give as the shape we want
end second model give us the holes placement
after this we get fully cade model for printing

# side quest 
While putting my own project aside for a while because I'm busy with college, I ended up helping my uncle to scan for his project (which I'll share here too). He faced a problem with the software:

```
[08:10:14.567179][info] Max number of threads regarding memory usage: 22
[08:10:14.567179][info] # threads for extraction: 22
```
_This is his error code._ 

The code indicates something to do with threads in his laptop, which is surprising because his laptop has a CPU that is better suited for handling workloads. But when I was researching it and doing the scan for him, I discovered that Meshroom really needs a lot of details about the camera and camera sensor (which are sometimes saved as part of the image file). If Meshroom recognizes these details, then it's all good, but if you use some niche camera or phone, it can cause problems. A lot of calculations for feature meshing and depth mapping are done by also having the focal length, which helps calculate the estimated distance from the sensor to the object.

I'll have an entire post dedicated to problems in [[Meshroom\|Meshroom]] and how to fix them, and also a bit of insight into 3D scanning and 3D in general.
# final thought
While this may be considered a failure, I do feel that I gained some insight into the fascinating world of 3D scanning. I plan to return to it someday as an enthusiastic 3D artist. However, for now, it seems that Meshroom isn't quite suited for precise 3D CAD work.

Feel free to check out my quick tutorial on Meshroom if it's already published. If not—I'm currently working on it!
[[cabinet/welcome_to_my_garden\|back to main page]]🏡