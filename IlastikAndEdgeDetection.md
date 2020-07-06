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




