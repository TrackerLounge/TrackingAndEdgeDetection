[Home Page](https://github.com/TrackerLounge/Home)

# Tracking and Edge Detection
Experiments to find edges of tracks. 

Computer Vision and Digital Image Signal Processing rely on edge detection and object segmentation to "make sense of the world".
I am interested in using computer vision techniques to automatically identify tracks in a scene, 3D scan, or set of pictures.

My motivation is from a hobby stance and outdoor enthusiast. However, there are practical applications. For example, in the UK it is estimated that half of all crime scenes have footprints collected in evidence and serves as a basic tool of criminal investigation there. In contrast, in the USA, the FBI estimates that some 6 or 7 million violent crimes occured in 2019. Of these, something like ~7000 footprints were collecected. See: https://www.youtube.com/watch?v=CyNocINOA7k (No affiliation)
These numbers probably reflect that collecting tracks is time consuming, costly and hard to do well. If this process could be simplified and/or automated to some degree, it may be a tool to aid in investigation.

As yet, I have not been successful. 
For examples of failures in machine learning see [Experiments with Image Processing, Computer Vision, and Machine Learning and Tracking](https://github.com/TrackerLounge/TrackingAndComputerVision)

Foot prints or tracks are difficult to perform edge detection on. Tracks are resistant to edge detection for many reasons, including:
- Tracks occur in 'noisy mediums' (e.g. dirt, dust, dew) of irregular hardness (e.g. mud next to rock)
- Tracks may be subtle, only be visible from viewing and lighting certain angles, relying on qualities of refection or dullness 
- Tracks may have very little differences in height from the "inside" of the track and the "outside" of the track, resulting in very weak edges
- Tracks can be made up of multiple appendages or areas, that may not be connected into a single unit when edge detected.
- Tracks are found on pitted, uneven surfaces and create uneven surfaces making it difficult to programatically define simple things like "ground level" or "elevation 0"

Also see https://www.youtube.com/watch?v=mPY8G-tCS1U (No affiliation)

This page will illustrate some approaches to edge detection. 

# Original Image
We have a track in our [tracking pit](https://github.com/TrackerLounge/ThreeBoxTrackingPitForTheHomeShop).
<img src='/images/CIMG2579.JPG' width=800>

<img src='/images/originalTrack.jpg' width=800>

# Edge Detection on Original Image
If we preform edge detection on this original image we get:

<img src='/images/originalTrack_edge_detect_sobel.jpg' width=800>

Edge detection on the original image tends to detect the edge around individual grains of sand rather than the edge of the track. If there are hard edges (e.g. leaves, branches, cracks, tile groute lines, etc.) these tend to be dominate the edge detection process, and obscure or ignore the track edge.

The track edge is clearly visible in the original image, to the naked eye. We need to find a process that will detect and highlight it.

# Preparing Track Images
[Color the Track along the Z-axis](https://github.com/TrackerLounge/TrackingAndEdgeDetection/blob/master/ColorTrackOnZAxis.md)

# Experiments with Different Approaches
[Thresholing and Edge Detection](https://github.com/TrackerLounge/TrackingAndEdgeDetection/blob/master/ThresholdAndEdgeDetection.md)

[Edge Detection by Segmentation](https://github.com/TrackerLounge/TrackingAndEdgeDetection/blob/master/EdgeDetectionBySegmentation.md)

[Fast Fourier Transform and Edge Detection](https://github.com/TrackerLounge/TrackingAndEdgeDetection/blob/master/FastFourierTransformAndEdgeDetection.md)

The FFT approach appears to be the most automatic and cleanest approach so far.

