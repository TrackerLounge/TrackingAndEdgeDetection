[Home Page](https://github.com/TrackerLounge/Home)

[Tracking and Edge Detection](https://github.com/TrackerLounge/TrackingAndEdgeDetection)

# Color the Track along the Z-Axis
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

The edge of the track is more visible now but it is still not strong enough to destinguish it automatically from the background noise.
