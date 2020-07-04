[Home Page](https://github.com/TrackerLounge/Home)

[Tracking and Edge Detection](https://github.com/TrackerLounge/TrackingAndEdgeDetection)

# Edge Detection by Segmentation
We will attempt to edge detect on a track that has been colored along the Z-axis. 
See: [Color the Track along the Z-axis](https://github.com/TrackerLounge/TrackingAndEdgeDetection/blob/master/ColorTrackOnZAxis.md)

ImageJ is a free tool with a number of powerful built-in image processing capabilities and many available plug-ins to enhances it's abilities.

We'll take a look at the "Make Binary" and "Segment by Particle" tools.

We will start with our track colored by the Z-axis

<img src='/imageJBinarySegmentation/trackColoredByZAxis_In_ImageJ.jpg' width=800>

Select Process>Binary>Make Binary

<img src='/imageJBinarySegmentation/imagej_binary_makeBinrary.jpg' width=800>

Here is the result of making the image binary

<img src='/imageJBinarySegmentation/trackColoredByZAxis_As_Binary_In_ImageJ.jpg' width=800>

Select Process>Find Maxima 

<img src='/imageJBinarySegmentation/imagej_process_find_maxima.jpg' width=800>

Select "Output Type" = "Segmented Particles" and click ok

<img src='/imageJBinarySegmentation/imagej_find_maxima_segmented_particals.jpg' width=800>

Here is the result:

<img src='/imageJBinarySegmentation/trackColoredByZAxis_As_Binary_Segmented_In_ImageJ.jpg' width=800>

In this case it isn't very good.

If we repeat the find_maxima but enable "light background":

<img src='/imageJBinarySegmentation/imagej_find_maxima_segmented_particals_light_background.jpg' width=800>

We get:

<img src='/imageJBinarySegmentation/trackColoredByZAxis_As_Binary_Segmented__white_background_In_ImageJ.jpg' width=800>

This is a little more intersting but doesn't provide a clean edge.


Compare to:

Track Colored by Z axis

<img src='/imageJBinarySegmentation/LF_20in_Stride_Wet_Sand_ColoredZAxis_Small.jpg' width=800>

Converted to Binary Image

<img src='/imageJBinarySegmentation/LF_20in_Stride_Wet_Sand_ColoredZAxis_Small_Binary_In_ImageJ.jpg' width=800>

Segmented by particles

<img src='/imageJBinarySegmentation/LF_20in_Stride_Wet_Sand_ColoredZAxis_Small_Binary_Segmented_In_ImageJ.jpg' width=800>

Segmented by particles with light background:

<img src='/imageJBinarySegmentation/LF_20in_Stride_Wet_Sand_ColoredZAxis_Small_Binary_Segmented_white_background_In_ImageJ.jpg' width=800>

And another example, where much of the pressure release has an elevation above the surrounding ground:

Track Colored by Z axis

<img src='/imageJBinarySegmentation/track01ColoredByZAxis_Small.jpg' width=800>

Converted to Binary Image

<img src='/imageJBinarySegmentation/track01ColoredByZAxis_Small_As_Binary_in_ImageJ.jpg' width=800>

Segmented by particles

<img src='/imageJBinarySegmentation/track01ColoredByZAxis_Small_As_Binary_Segmentation_in_ImageJ.jpg' width=800>

Segmented by particles with light background:

<img src='/imageJBinarySegmentation/track01ColoredByZAxis_Small_As_Binary_Segmentation__light_background_in_ImageJ.jpg' width=800>

The segmentation process produces interesting results which may be worth explerimenting with further. It may be useful as part of a track processing pipeline.
