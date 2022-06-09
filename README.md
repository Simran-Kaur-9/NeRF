# NeRF


[NeRF](http://www.matthewtancik.com/nerf) (Neural Radiance Fields) NeRF is a method for generating novel views of complex scene. It takes
a set of input images of a scene and renders the complete scene by interpolating between the 
scenes.
<br>
The output is a volume whose color and density are dependent on the direction of the camera rays and the emitted light radiance at that point. For each ray we generate an output volume and all these volume make up the complex scene.


## ARCHITECTURE OF NeRF

![pipeline](https://user-images.githubusercontent.com/42802893/172758710-d5f3d598-1986-4435-b25e-7e98caddc87e.jpg)

A static scene is represented as a continuous 5D function as defined above. The method uses a fully connected neural network- a multilayered perceptron(MLP) to represent this function by moving backward from a single 5D coordinate (x, y, z, θ, φ) to output a volume density (with RGB color influenced by view)



## VOLUME RENDERING

Volume rendering enables you to create a <b>2D projection</b> of a <b>3D discretely sampled dataset</b>.

For a given camera position, a volume rendering algorithm obtains the RGBα (Red, Green, Blue, and Alpha channel) for every voxels in the space through which rays from the camera are casted.  The RGBα color is converted to an RGB color and recorded in the corresponding pixel of the 2D image. The process is repeated for every pixel until the entire 2D image is rendered.


## DATA PREPROCESSING

Our method includes using [LLFF](https://github.com/fyusion/llff) which takes in a set of images of a static scene, promotes each image to a local layered representation (MPI), and blends local light fields rendered from these MPIs to render novel views

This helps us to generate the input vector for different projections of a custom image


## WORKING OF NeRF

<ol>
<li><b>Generate a sampled set of 3D points</b>—by marching camera rays through the scene.</li>
<li><b>Produce an output set of densities and colors</b>—by inputting your sampled points with their corresponding 2D viewing directions into the neural network.</li>
  <li><b>Accumulate your densities and colors into a 2D image</b>—by using classical volume rendering techniques.</li>
</ol>

The process above optimizes a deep, fully-connected, multi-layer perceptron (MLP) but does not require using convolutional layers. It uses gradient descent to minimize errors between each observed image and all corresponding views rendered from the representation.


## SAMPLE RESULTS FROM TRAINING(~36hr training config)

![fern_output_AdobeCreativeCloudExpress](https://user-images.githubusercontent.com/56038663/172764877-62fe00b9-eceb-4c99-9b37-0f8904b1ba6d.gif)



## APPLICATIONS OF NeRF
<ul>
  <li><b>Lots of tourists take lots of photographs. And these photographs can be used to render complex photorealistic scenes.</li>
  <li><b>Recently, NeRF has been extended to NR-NeRF (non-rigid NeRF). While NeRF is used for photorealistic appearance and geometry reconstruction of static scenes, NR-NeRF deals with non-rigid dynamic scenes.</li>
  <li><b>NeRF is good with complex geometries and deals with occlusion well.</li>
  <li><b>It can be used to generate mesh view of an object.</li>
  <li><b>Relighting: We extend NeRF to enable the rendering of scenes from novel viewpoints under arbitrary lighting conditions.</li>
  <li><b>It can be used for Human Modelling</li>
 </ul>
 
![Human_modelling_AdobeExpress](https://user-images.githubusercontent.com/56038663/172765906-89e8e619-340b-42b6-b0a2-85c45317c528.gif)  


