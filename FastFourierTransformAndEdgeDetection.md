[Home Page](https://github.com/TrackerLounge/Home)

[Tracking and Edge Detection](https://github.com/TrackerLounge/TrackingAndEdgeDetection)

# Fast Fourier Transform and Edge Detection
We will attempt to edge detect on a track that has been colored along the Z-axis. 
See: [Color the Track along the Z-axis](https://github.com/TrackerLounge/TrackingAndEdgeDetection/blob/master/ColorTrackOnZAxis.md)

[ImageJ](https://imagej.nih.gov/ij/index.html) is a free tool with a number of powerful built-in image processing capabilities and many available plug-ins to enhances it's abilities. [ImageJ Wiki](https://en.wikipedia.org/wiki/ImageJ)

We'll take a look at the FFT (Fast Fourier Transform) functionality.

For an introduction on Fourier Transform, I would recommend watching 3Blue1Brown's excellent youtube video (no relationship) on the subject - [But what is the Fourier Transform? A visual introduction](https://www.youtube.com/watch?v=spUNpyF58BY)

We will do the following to our test images:
1. Apply FFT Bandpass Filter
2. Convert Resulting Image To Binary

To run the FFT Bandpass Filter click Process > FFT > Bandpass Filter
<img src='/imageJFFT/imageJ_FFT_BandpassFilter.jpg' width=800>

In the FFT Bandpass Filter dialog you can set several settings. We will focus on three:
- Filter large structures down to:
- Filter small structures up to 
- Display filter
<img src='/imageJFFT/FFTBandpassFilter.jpg' width=800>

In general the smaller the "Filter large structures down to" value is set to the more segmented lorge structures will be.
In general the larger the "Filter large structures down to" value is set to the more consolidated lorge structures will be.
Play around with this value. In these test cases I will be using a value of 600 pixels.

For example here are three results, using different values for "Filter large structures down to".

<img src='/imageJFFT/FFTBandpassFilterCompare40.jpg' width=800>

<img src='/imageJFFT/FFTBandpassFilterCompare100.jpg' width=800>

<img src='/imageJFFT/FFTBandpassFilterCompare300.jpg' width=800>

Notice that as the value goes up, we capture more and more of the total track.
FFT works with frequencies. Imaging that you are looking at the track from the side, line of the track rises and falls in a 2D space. The track would represent a large low frequency in this graph. The bumpy soil would represent lots of high frequency jitters. I think of the "Filter large structures down to" setting allowing to to say "I want to focus more on the BIG frequency of the track rather than the small high frequency noisy surface of the soil. Is this a correct view. I really don't know.

In general the smaller the "Filter small structures up to" value is set to the noiser and more speckled your result will be.
In general the larger the "Filter small structures up to" value is set to the smoother and cleaner result will be.
Play around with this value. In these test cases I will be using a value of 10 pixels.

For example here are three results, using different values for "Filter small structures up to".

<img src='/imageJFFT/FFTBandpassFilterCompare600_3.jpg' width=800>

<img src='/imageJFFT/FFTBandpassFilterCompare600_10.jpg' width=800>

If you want to see what the FFT filter looks like, check the display filter.
When you run the Bandpass filter, it will open another window to show the filter.

<img src='/imageJFFT/FFT_Filter.jpg' width=800>

This is also useful, when building up a filter. ImageJ allows you to add multiple filters together in the Process > FFT > Custom Filter. 
It allows you to select any of the image windows that you have open. 
You may run Process > FFT > Bandpass Filter and display filter. It will get a name like "Filter". 
You may run Process > FFT > Bandpass Filter with a second set of values and display filter. It will get a name like "Filter(1)".
With these two filter windows open, in Process > FFT > Custom Filter, you can add them together or subtract one from the other or inverse them to create a more complex filter.

For now we will work with a single filter.

# Optional
We could convolve the binary images to narrow in on the specific edge if we wanted to.

<img src='/imageJFFT/imageJ_process_filter_convolve.jpg' width=800>

<img src='/imageJFFT/convolve_kernel.jpg' width=800>


# Results.

## Test 1
Image colored along Z axis:

<img src='/imageJFFT/LF_20in_Stride_Wet_Sand_ColoredZAxis_Small.jpg' width=800>

FFT Bandpass filtered Image:

<img src='/imageJFFT/LF_20in_Stride_Wet_Sand_ColoredZAxis_Small_FFT_Bandpass.jpg' width=800>

FFT Bandpass filtered Image converted to Binary Image:

<img src='/imageJFFT/LF_20in_Stride_Wet_Sand_ColoredZAxis_Small_FFT_Bandpass_make_binary.jpg' width=800>

Filter using Convolve kernel:

<img src='/imageJFFT/LF_20in_Stride_Wet_Sand_ColoredZAxis_Small_FFT_Bandpass_make_binary_convolved.jpg' width=800>

## Test 2
Image colored along Z axis:

<img src='/imageJFFT/track01ColoredByZAxis_Small.jpg' width=800>

FFT Bandpass filtered Image:

<img src='/imageJFFT/track01ColoredByZAxis_Small_FFT_Bandpass.jpg' width=800>

FFT Bandpass filtered Image converted to Binary Image:

<img src='/imageJFFT/track01ColoredByZAxis_Small_FFT_Bandpass_make_binary.jpg' width=800>

## Test 3
Image colored along Z axis:

<img src='/imageJFFT/trackColoredByZAxis.jpg' width=800>

FFT Bandpass filtered Image:

<img src='/imageJFFT/trackColoredByZAxis_FFT_Bandpass.jpg' width=800>

FFT Bandpass filtered Image converted to Binary Image:

<img src='/imageJFFT/trackColoredByZAxis_FFT_Bandpass_Make_Binary.jpg' width=800>

# Conclusion/Observations
Overall, this approach appears to produce pretty decent object and edge detection. I did have to manually play around with the High and low value in the FFT Bandpass filter until I found value that worked adequately for all three images. This range could be played with more. It would be interesting to see if this range works well on a wider set of test images. 

I suspect we would need a series of FFT processes - one to find the regions of interest in the image where the track is, then others to get greater details about the structures within the identified track. Once you have the rough outline of the track, you can then mask away the ground surface outside the track in the original image and re-run the FFT process again with different settings to get finer details inside the track to capture shoe sole patterns or pressure release structures in finer detail. 

Note: this performs less well if the FFT filtered object is allowed to be noisy and/or when the pressure releases appear outside the track as in example 2.

But...before we finish...you may be wondering how this approach would work on our original image.
So here are the results.

Here is the original image

<img src='/imageJFFT/originalTrack_Small01.jpg' width=800>

Here is the FFT Bandpass filtered Image converted to Binary Image:

<img src='/imageJFFT/originalTrack_small_FTT_Bandpass_Make_Binary.jpg' width=800>

As you can see, it does not produce a good result on the original image. It really focuses on the shadowed areas. 

In order for the FFT approach to work, we need to be working with a colored track - [Color the Track along the Z-axis](https://github.com/TrackerLounge/TrackingAndEdgeDetection/blob/master/ColorTrackOnZAxis.md)

Perhaps this approach could be made to work with uncolored images, if we took images, with a flash firing from several sides (say 12 o'clock, 3 o'clock, 6 o'clock, and 9 o'clock) and then merged the resulting images together. Hopefully that would create enough shadows to highlight the topography. We might have enough contrast to make this work better. In the past, I played around with this approach and wasn't successful but ... ya never know.
Also, perhaps more twittling with the High and Low value in the FFT Bandpass filter would produce a better result? I kinda doubt it but might be interesting to try out.




