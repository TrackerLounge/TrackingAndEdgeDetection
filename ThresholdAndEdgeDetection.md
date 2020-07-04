[Home Page](https://github.com/TrackerLounge/Home)

[Tracking and Edge Detection](https://github.com/TrackerLounge/TrackingAndEdgeDetection)

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

For more examples of edge detection on tracks see:
[Fast Walk - Edge detection on track 01](https://github.com/TrackerLounge/DigitalTrackingPit/blob/master/FastWalk.md)

Unfortunately, there are too many manual (and subjective) steps in this process. This process also relies on having a 3D digital model of the track (which would add processing time and expense to the process.)
