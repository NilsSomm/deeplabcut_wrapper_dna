# deeplabcut_wrapper_dna
Install Cuda (technically optional, but training will be slow otherwise) https://docs.nvidia.com/cuda/cuda-installation-guide-microsoft-windows/index.html
	Also, this is only if your machine has an Nvidia gpu. If it prompts you that no version of vsCode is found and that you won’t have full functionality without it, make sure you download vsCode and try to reinstall with it finding vsCode.

Install pytorch https://pytorch.org/get-started/locally/
	The “start locally” command is important at the beginning after you installed Cuda.

You’ll want to confirm that cuda and pytorch are connected. Run something like the code below in python:
import torch
torch.cuda.is_available()
This should return true.

Install imageMagick (optional) https://imagemagick.org/index.php
	Only needed if you want to batch convert .tif files to .png, I find this useful when doing analysis of TEM image crops using the imageJ macro Michael N. made https://github.com/MNeuhoff/Crop-and-Collage-Tools

Install deeplabcut https://deeplabcut.github.io/DeepLabCut/docs/installation.html
	I used the conda installation process, specifically step 2 is the important one, where you download the yaml file and create the virtual environment.

Download Bulk Rename Utility (optional) https://www.bulkrenameutility.co.uk/Download.php
	This is to rename files in bulk, which can be handy if we are creating a large training set with files that might have the same name at first.

First, let's make a folder of our training data. Both sections below (ImageMagick and Bulk Rename Utility) might be useful for this

Batch converting .tif to .png with ImageMagick:
Create a folder with all of your .tif files
Inside this folder, create another folder called “png_files”.
In a windows terminal, navigate to the folder containing the .tif files and the other folder
Run the command: for %f in (*.tif) do magick "%f" "png_files\%~nf.png"
You will see that “png_files” contains your converted png files, which will work in deeplabcut

Using Bulk Rename Utility
Launch Bulk Rename Utility, just search it on the windows bar. There will be a lot going on but only a few things are relevant for what we want to do.
Navigate to the folder with the images you want to rename.
On the tab “Name (2)”, select “Fixed” for the dropdown “Name”, and below enter your filename.
On the tab “Numbering (10)”, select “Suffix” for “Mode”
On the tab “Numbering (10)”, change padding such that each of your files can get a unique file name (ie. for <=100 files, padding is 3, for >100 and <=1000 padding is 4, etc.)
Select all files in your folder you want to rename (ctrl+A to select all)
Press “Rename” at the bottom right and press OK.
Your files should now be renamed with an appropriate suffix.

Checks/Troubleshooting
Try running the check if cuda is available in your DEEPLABCUT environment as well
When you are training the network, check your gpu in task manager, and see if its memory is being used.
