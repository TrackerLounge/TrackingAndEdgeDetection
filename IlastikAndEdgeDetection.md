[Home Page](https://github.com/TrackerLounge/Home)

[Tracking and Edge Detection](https://github.com/TrackerLounge/TrackingAndEdgeDetection)

# Ilastik and Edge Detection
[Ilastik](https://www.ilastik.org/) is a free opensource tool.
Ilasktik has many capabilities. We will be experimenting with Image Segmentation and Pixel Classification.
For a introduction to Ilastick see the youtube video [Image Segmentation with ilastick - Pixel Classification](https://www.youtube.com/watch?v=MaPareZNvCw)

We will attempt to edge detect on a track that has been colored along the Z-axis. 
See: [Color the Track along the Z-axis](https://github.com/TrackerLounge/TrackingAndEdgeDetection/blob/master/ColorTrackOnZAxis.md)

We will provide ilastik with several tracks colored on along the Z-axis and tell ilastik which parts of the images are the "track" and which parts of the image are the background.
Ilastik will then try lots of Guassian Blurs on the image and try to figure out which blurs and edge detection best highlight the parts of the image that we labeled as "track".
After training, ilastik will ask for one or more new images that it has never seen before. Ilastik will then try the best Guassian Blurs and Edge Detection settings (from the training set of images) on the new images.
Ilastik will produce image masks for each of the new images. The mask will have two colors in it - black and white - one should cover all of the areas in the image that ilastik thinks is a track and the other will cover all areas in the image that ilastik thinks is "background".

# Ilastik Example
We have a few files to test with:
<img src='/ilastikFiles/testFiles.jpg' width=800>

Download the [images](https://github.com/TrackerLounge/TrackingAndEdgeDetection/tree/master/ilastikFiles/images)

We will use 3 files for training and 3 files for testing later on.

On the ilastik main page, select "Pixel Classification":

<img src='/ilastikFiles/ilastik_main_menu.jpg' width=800>

ilastik will ask you to create a project file

<img src='/ilastikFiles/new_ilastik_project.jpg' width=800>

ilastik will ask you to import some of your test files. Click "Add New" and select 3 of our track images colored along the z-axis.

<img src='/ilastikFiles/ilastik_step01_add_files.jpg' width=800>

<img src='/ilastikFiles/ilastik_step01_files_imported.jpg' width=800>

Next, click on "2. Feature Selection" on the left side of the screen.

You will be asked to "Select Features"

<img src='/ilastikFiles/ilastik_step02_feature_selection.jpg' width=800>

ilastik will provide you with a popup menu like this:

<img src='/ilastikFiles/ilastik_step02_feature_selection_popup01.jpg' width=800>

Each box that you check will cause ilastik to create a series of files at that range. These files will then be used by ilastik to train on. ilastik will try to see which of these files best find and match the elements that you highlighted in the images.

I will select them all for now.

<img src='/ilastikFiles/ilastik_step02_feature_selection_popup02.jpg' width=800>

Click ok. ilastik will generate the files you selected.

ilastik will auto-generate multiple Gaussian Smoothing images for each of our test files. You can click on the left side images to see the results.

<img src='/ilastikFiles/ilastik_step02_feature_selection_MultipleGaussianSmoothing.jpg' width=800>

ilastik will auto-generate multiple Laplacian Of Gaussian images for each of our test files. You can click on the left side images to see the results.

<img src='/ilastikFiles/ilastik_step02_feature_selection_MultipleLaplacianOfGaussian.jpg' width=800>

ilastik will auto-generate multiple Gaussian Gradient Magnitude images for each of our test files. You can click on the left side images to see the results.

<img src='/ilastikFiles/ilastik_step02_feature_selection_MultipleGaussianGradientMagnitude.jpg' width=800>

ilastik will auto-generate multiple Difference of Gaussians images for each of our test files. You can click on the left side images to see the results.

<img src='/ilastikFiles/ilastik_step02_feature_selection_MultipleDifferenceOfGaussians.jpg' width=800>

ilastik will auto-generate multiple Structure Tensor Eigenvalues images for each of our test files. You can click on the left side images to see the results.

<img src='/ilastikFiles/ilastik_step02_feature_selection_MultipleStructureTensorEigenvalues.jpg' width=800>

ilastik will auto-generate multiple Hessian of Gaussian Eigenvalues images for each of our test files. You can click on the left side images to see the results.

<img src='/ilastikFiles/ilastik_step02_feature_selection_MultipleHessianOfGaussianEigenvalues.jpg' width=800>

Next, click on "3. Training" on the left side of the screen.

<img src='/ilastikFiles/ilastik_step03_training.jpg' width=800>

You can see in the left side of the screen "Label 1" and "Label 2". 
I will change "Label 1" to "track"
I will cahnge "Label 2" to "ground"

<img src='/ilastikFiles/ilastik_step03_training_labels.jpg' width=800>

With the "track" label selected, draw on the image to indicate what you would consider the areas of the track. It will show up as a yellow line.

<img src='/ilastikFiles/ilastik_step03_training_track_highlight01.jpg' width=800>

With the "ground" label selected, draw on the image to indicate what you would consider the areas of the ground. It will show up as a blue line.

<img src='/ilastikFiles/ilastik_step03_training_track_highlight02.jpg' width=800>

Click "Live Update" for it to compare what you have drawn to the pre-prepared Gaussian/Laplacian/Edge images. It will color your image blue or yellow and indicate where it might still think something is track when it is ground or ground when it is track.

<img src='/ilastikFiles/ilastik_step03_training_track_highlight03.jpg' width=800>

On the left side change the image by selecting the next image in the "current view" drop down. 

Repeat the process of labeling the "track" and "ground" in the other training images. If the images are already highlighted well enough you can move to the next step.

Click "Live Update" again to stop it.

Click "4. Prediction Export"

<img src='/ilastikFiles/ilastik_step04_prediction_export.jpg' width=800>

Change the Source to "Simple Segmentation"

<img src='/ilastikFiles/ilastik_step04_prediction_export02.jpg' width=800>

Click on "Choose Export Image Settings"

In the popup, click Format: JPEG (or whatever you want).
Note: After working throught this trial, I went back and tried the file type .tif and found that it had better resolution. Not sure why. 

<img src='/ilastikFiles/ilastik_step04_prediction_export02_popup.jpg' width=800>

Click ok

Click "5. Batch Processing"

<img src='/ilastikFiles/ilastik_step05_batch_processing.jpg' width=800>

Select Raw Data Files
Select the files you want ilastik to try what it has learned on. We will select the 3 track files that we didn't use during the training phase.

<img src='/ilastikFiles/trialImages.jpg' width=800>

You should now see the files in ilastik. 
When we click "Process all files", ilastik should create a mask file in the file system for each of the 3 files we just selected.

<img src='/ilastikFiles/ilastik_step05_batch_processing02.jpg' width=800>

<img src='/ilastikFiles/ilastik_generated_mask_files.jpg' width=800>

In Gimp, we will open a test image.

<img src='/ilastikFiles/testTrack01.jpg' width=800>

We will then add a layer on the image and drag in the mask for that image. 
Make the opacity of the new layer 50%.
Right click on the layer and merge down. 

Click on Color > Auto > White Balance

<img src='/ilastikFiles/testTrack01_ApplyWhiteBalance.jpg' width=800>

The white is what ilastik thought of as the ground in the images that it had never seen before.

<img src='/ilastikFiles/testTrack01_WhiteBalance.jpg' width=800>

<img src='/ilastikFiles/testTrack02_WhiteBalance.jpg' width=800>

<img src='/ilastikFiles/testTrack03_WhiteBalance.jpg' width=800>

# Conclusion
The results are interesting but not very good for our purposes. Perhaps with more training images, more pre-prepared Gaussian ranges, and more labeling, we might be able to get better results.

If we could get better results, perhaps this could be useful in our pre-processing pipeline.
For now, it is useful to quickly get a feeling for what some default Gaussian ranges will see. This prompted me to play around more with the ranges in Fast Fourier Transform (FFT) and get better results.

Also note: I am new to ilastik. There are lots of great training resources available on it and many powerful tools in it. My poor results could simply be due to my inexperience with the tool or using the wrong tool in Ilastik for this problem space. I am interested in playing with other tools in ilastik to learn more. For example Classification looks intreguing [ilastik 0.5: Introduction to Classification](https://www.youtube.com/watch?v=9fzDI_ayOJ4) 
