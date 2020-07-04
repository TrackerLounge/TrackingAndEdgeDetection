[Home Page](https://github.com/TrackerLounge/Home)

[Tracking and Edge Detection](https://github.com/TrackerLounge/TrackingAndEdgeDetection)

# Fast Fourier Transform and Edge Detection
We will attempt to edge detect on a track that has been colored along the Z-axis. 
See: [Color the Track along the Z-axis](https://github.com/TrackerLounge/TrackingAndEdgeDetection/blob/master/ColorTrackOnZAxis.md)

ImageJ is a free tool with a number of powerful built-in image processing capabilities and many available plug-ins to enhances it's abilities.

We'll take a look at the FFT (Fast Fourier Transform) functionality.

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

In general the smaller the "Filter small structures up to" value is set to the noiser and more speckled your result will be.
In general the larger the "Filter small structures up to" value is set to the smoother and cleaner result will be.
Play around with this value. In these test cases I will be using a value of 10 pixels.

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
Overall, this approach appears to produce pretty decent object and edge detection. 
Though this performs less well if the FFT filtered object is allowed to be noisy and/or when the pressure releases appear outside the track as in example 2.






