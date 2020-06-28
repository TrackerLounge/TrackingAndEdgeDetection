[Home Page](https://github.com/TrackerLounge/Home)

# Tracking and Edge Detection
Experiments to find edges of tracks. 

Computer Vision and Digital Image Signal Processing rely on edge detection and object segmentation to "make sense of the world".
I am interested in using computer vision techniques to automatically identify tracks in a scene, 3D scan, or set of pictures.

My motivation is from a hobby stance and outdoor enthusiast. However, there are practical applications. For example, in the UK it is estimated that half of all crime scenes have footprints collected in evidence and serves as a basic tool of criminal investigation there. In contrast, in the USA, the FBI estimates that some 6 or 7 million violent crimes occured in 2019. Of these, ~7000 footprints were collecected. These numbers probably reflect that collecting tracks is time consuming, costly and hard to do well. If this process could be simplified and/or automated to some degree, it may be a tool to aid in investigation.

As yet, I have not been successful. 
For examples of failures in machine learning see [Experiments with Image Processing, Computer Vision, and Machine Learning and Tracking](https://github.com/TrackerLounge/TrackingAndComputerVision)

Foot prints or tracks are difficult to perform edge detection on. Tracks are resistant to edge detection for many reasons, including:
- Tracks occur in 'noisy mediums' (e.g. dirt, dust, dew)
- Tracks may be subtle, only be visible from viewing and lighting certain angles, relying on qualities of refection or dullness 
- Tracks may have very little differences in height from the "inside" of the track and the "outside" of the track, resulting in very weak edges
- Tracks can be made up of multiple appendages or areas, that may not be connected into a single unit when edge detected.
- Tracks are found on pitted, uneven surfaces and create uneven surfaces making it difficult to programatically define simple things like "ground level" or "elevation 0"

This page will illustrate some approaches to edge detection. 

# Original Image
We have a track in our [tracking pit](https://github.com/TrackerLounge/ThreeBoxTrackingPitForTheHomeShop).
<img src='/images/CIMG2579.JPG' width=800>

<img src='/images/originalTrack.jpg' width=800>

# Edge Detection on Original Image
If we preform edge detection on this original image we get:
<img src='/images/originalTrack_edge_detect_sobel.jpg' width=800>

# Convert Image to 3D Model
If we convert the Image to a 3D model using [Tracking and Photogrammetry](https://github.com/TrackerLounge/TrackingAndPhotogrammetry)
We have a lot more control of elevation, lighting, and coloration that may help us in edge detection.

For example, we can color the 3D model based on elevation or the Z-Axis.
<img src='/images/modelOfTrackColoredByZAxisInBlender.jpg' width=800>

If you want to play around with the model in blender, you can download the zip compressed blender file from:
<a id="raw-url" href="https://raw.githubusercontent.com/TrackerLounge/TrackingAndEdgeDetection/master/blender/track_colored_by_z_axis.zip">Download FILE - track_colored_by_z_axis.zip</a>

[track.zip Compressed Blender File](blender/track_colored_by_z_axis.zip)

<img src='/images/trackColoredByZAxis.jpg' width=800>

If we were to sobel edge detect on this image, we would see something like
<img src='/images/trackColoredByZAxis_edgeDetect_sobel.jpg' width=800>

# Edge Detection on the Track Colored in the Z-Axis
In Gimp, we can quickly experiment with lots of potential image procesing pipelines.

For example we may try the following:
1. Threshold the image manually to create a strong edge.
2. Dilate the image to remove remaining pixelation and noise.
3. Edge detect 
4. Color largest objects manually

Here is what that might look like

In Gimp, when you threshold an image it will try to automatically find the right level.

<img src='/images/trackColoredByZAxis_autoThreshold.jpg' width=800>

If we manually adjust the threshold we can isolate to main objects with strong edges.

<img src='/images/trackColoredByZAxis_manualThreshold.jpg' width=800>

We can manually dilate the image 3 times to fill in the pixelation and reduce overall noise.

<img src='/images/trackColoredByZAxisManualThresholdAndDilated3Times.jpg' width=800>

We can run Edge Detection on the despecaled, thresholded image. I used Sobel edge detection here (it is the default). You can play around with all of the different edge detection algorithms to see which one works best in your situation. In my case these didn't seem to be a clear winner.

<img src='/images/trackColoredByZAxisManualThresholdAndDilated3TimesEdgeDetectedSobel.jpg' width=800>

This produces:

<img src='/images/trackColoredByZAxisManualThresholdAndDilated3TimesEdgeDetectedSobelResult.jpg' width=800>

I can then manually fill the large artifacts in the image to ensure that the edges all connect.

<img src='/images/trackEdgeFilled.jpg' width=800>

Unfortunately, there are too many manual (and subjective) steps in this process. This process also relies on having a 3D digital model of the track (which would add processing time and expense to the process.)
