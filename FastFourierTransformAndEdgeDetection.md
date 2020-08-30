[Home Page](https://github.com/TrackerLounge/Home)

[Tracking and Edge Detection](https://github.com/TrackerLounge/TrackingAndEdgeDetection)

# Fast Fourier Transform and Edge Detection
We will attempt to edge detect on a track that has been colored along the Z-axis. 
See: [Color the Track along the Z-axis](https://github.com/TrackerLounge/TrackingAndEdgeDetection/blob/master/ColorTrackOnZAxis.md)

[ImageJ Welcome Page](https://imagej.net/Welcome)

[ImageJ](https://imagej.nih.gov/ij/index.html) is a free tool with a number of powerful built-in image processing capabilities and many available plug-ins to enhances it's abilities. [ImageJ Wiki](https://en.wikipedia.org/wiki/ImageJ)

We'll take a look at the FFT (Fast Fourier Transform) functionality.

For an introduction on Fourier Transform, I would recommend watching 3Blue1Brown's excellent youtube video (no relationship) on the subject - [But what is the Fourier Transform? A visual introduction](https://www.youtube.com/watch?v=spUNpyF58BY)

We will do the following to our test images:
1. Apply FFT Bandpass Filter
2. Convert Resulting Image To Binary

To run the FFT Bandpass Filter click Process > FFT > Bandpass Filter
<img src='/imageJFFT/imageJ_FFT_BandpassFilter.jpg' width=800>

[ImageJ Source Code](https://imagej.nih.gov/ij/developer/source/)

Not sure of best place to download source all source code - could start here:

[Github for Imagej - ImageJA](https://github.com/imagej/ImageJA)

[ImageJ Sourc Code for FFTFilter Class](https://imagej.nih.gov/ij/developer/source/ij/plugin/filter/FFTFilter.java.html)

[Description of ImageJ FFT Filter Plugin](https://imagej.nih.gov/ij/plugins/fft-filter.html)

Here is a rough approximation in Java (note: I can't figure out how to invert the resulting image yet)
```java
package org.trackerlounge;

import java.io.File;
import java.nio.file.Path;
import java.nio.file.Paths;

import ij.IJ;
import ij.ImagePlus;
import ij.plugin.LutLoader;
import ij.plugin.Thresholder;
import ij.plugin.filter.FFTFilter;
import ij.process.ImageProcessor;

//Download ImageJ exe. It will come with ij.jar. Add that to your project library path.

//https://github.com/imagej/ImageJA/blob/master/src/main/java/ij/plugin/filter/FFTFilter.java
//https://imagej.nih.gov/ij/developer/source/
//https://github.com/imagej/ImageJA

//https://imagej.nih.gov/ij/developer/source/ij/plugin/filter/FFTFilter.java.html
//https://imagej.nih.gov/ij/developer/api/ij/plugin/filter/FFTFilter.html

//https://imagej.nih.gov/ij/developer/api/ij/ImagePlus.html
//https://imagej.nih.gov/ij/developer/api/ij/IJ.html

//https://imagej.nih.gov/ij/developer/source/ij/plugin/Thresholder.java.html
//https://imagej.nih.gov/ij/developer/api/ij/plugin/Thresholder.html

//https://imagej.nih.gov/ij/developer/source/ij/plugin/LutLoader.java.html
//https://imagej.nih.gov/ij/developer/api/ij/plugin/LutLoader.html
public class BPInOpenCV {
	
	public static void main(String[] args) throws Exception {
		Path currentRelativePath = Paths.get("");
		String s = currentRelativePath.toAbsolutePath().toString();
		System.out.println("Current relative path is: " + s);
		String path = s+"\\resources\\";
		
		String fileName = "LF_20in_Stride_Wet_Sand_ColoredZAxis_Small.jpg";
		File file = new File(path, fileName);
		
		ImagePlus imp = new ImagePlus(file.getAbsolutePath());
		String arg = "";//Don't know what this should be
		
		FFTFilter f = new FFTFilter();
		f.setup(arg, imp);
		
		ImageProcessor ip = imp.getChannelProcessor();
		f.run(ip);
		imp.show();
		//https://imagej.nih.gov/ij/developer/api/ij/IJ.html#save-ij.ImagePlus-java.lang.String-
		String result = path+"\\band_pass_filter.jpg";
		IJ.save(imp, result);
	
		// Not sure how to invert the image correctly - I think I should invert the LUT but this doesn't seem to take effect.
		/* Output is a binary image, with foreground 255 and background 0, using an inverted or normal LUT depending on the 
		 * "Black Background" option in Process>Binary>Options. The number of particles (as obtained by "Analyze Particles") 
		 * in the output image does not depend on the "Output Type" selected. Note that "Segmented Particles" will usually 
		 * result in particles touching the edge if "Exclude Edge Maxima" is selected. "Exclude Edge Maxima" applies to the 
		 * maximum, not to the particle.
		 */		
		LutLoader lutLoader = new LutLoader();
		lutLoader.run("invert");
		
		
		//Not sure how to set the IJ.setImage() - this seems to be set by IJ.save()???
		Thresholder t = new Thresholder();
		String arg3="";
		t.run(arg3);
		imp.show();
		String result3 = path+"\\binary_result.jpg";
		IJ.save(IJ.getImage(), result3);
	
	}
	
}
```
For a youtube video on this see
/imageJFFT/runningImageJInYourJavaCodeTitleScreen.jpg
[![Alt text](https://github.com/TrackerLounge/TrackingAndEdgeDetection/blob/master/imageJFFT/runningImageJInYourJavaCodeTitleScreen.jpg)](https://www.youtube.com/watch?xc3syeTIv-k)

To run the Make Binary Image click Process > Binary > Make Binary
<img src='/imageJFFT/imagej_binary_makeBinrary.jpg' width=800>

[ImageJ Sourc Code for Binary Class](https://imagej.nih.gov/ij/developer/source/ij/plugin/filter/Binary.java.html)

In the FFT Bandpass Filter dialog you can set several settings. We will focus on three:
- Filter large structures down to:
- Filter small structures up to 
- Display filter
<img src='/imageJFFT/FFTBandpassFilter.jpg' width=800>

In general the smaller the "Filter large structures down to" value is set to the more segmented lorge structures will be.
In general the larger the "Filter large structures down to" value is set to the more consolidated lorge structures will be.
Play around with this value. In these test cases I will be using a value of 600 pixels.

For example here are three results (after appling FFT Bandpass Filter and Make Binary), using different values for "Filter large structures down to".

<img src='/imageJFFT/FFTBandpassFilterCompare40.jpg' width=800>

<img src='/imageJFFT/FFTBandpassFilterCompare100.jpg' width=800>

<img src='/imageJFFT/FFTBandpassFilterCompare300.jpg' width=800>

Notice that as the value goes up, we capture more and more of the total track.
FFT works with frequencies. Imaging that you are looking at the track from the side, line of the track rises and falls in a 2D space. The track would represent a large low frequency in this graph. The bumpy soil would represent lots of high frequency jitters. I think of the "Filter large structures down to" setting allowing to to say "I want to focus more on the BIG frequency of the track rather than the small high frequency noisy surface of the soil. Is this a correct view. I really don't know.

Note: In soft soil, where the track creates deep impressions, the track is likely the represent the biggest frequency (sine curve) if you were to look at the track and surrounding ground from the side view. In this case you want to use a large value (e.g. 600) for "Filter large structures down to". However, as the surface becomes harder and the track less deep, the track may represent a much less pronounced curve than the curve made up by the uneven ground. In this case, you'd want to use a smaler value (e.g 40 to 100) for the "Filter large structures down to". As the surface becomes harder and the soil depth becomes thinner it becomes harder and harder for a standard Bandpass FFT filter to seperate the track from the surrounding ground. You can try to boost the track visibility by scaling the 3D model in the Z axis before shading it along the Z-axis. In some cases this can aid in seeing tracks in shallower soil and dust. However, it tends to warp and twist the 3D model in odd ways and can make lighting the model more challenging with more numerous small troughs and channels that need lighting. For a visual comparison of the same track in different soils  and the FFT edges in those different soils see [Left Foot 20 Inch Stride](https://github.com/TrackerLounge/DigitalTrackingPit/blob/master/LeftFoot20InchStride.md)

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

Alternatively we could combine two FFT using different "Filter large structures down to" values to produce a result.

<img src='/imageJFFT/LF_20in_Stride_Wet_Sand_ColoredZAxis_Small_FFT_combined_as_mask.jpg' width=800>

Resulting in  something like:

<img src='/imageJFFT/LF_20in_Stride_Wet_Sand_ColoredZAxis_Small_masked_2_FFT.jpg' width=800>

Or we could use it as a mask on the original image colored on the z axis

<img src='/imageJFFT/LF_20in_Stride_Wet_Sand_ColoredZAxis_Small_masked.jpg' width=800>

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
Overall, this approach appears to produce pretty decent object and edge detection in soft substraits/soils where the tracks are deep. I did have to manually play around with the High and low value in the FFT Bandpass filter until I found value that worked adequately for all three images. This range could be played with more. It would be interesting to see if this range works well on a wider set of test images. However, this general approach starts to fall apart in harder substraits/soils, where the track is very shallow and/or the ground has larger undulations/unevenness than the track. 

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




