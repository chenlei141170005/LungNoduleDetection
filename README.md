# LungNoduleDetection
This project follows the LungCancerProject.
Deep learning is a very hot field and it has promising application in medical image. 
Now the medical image is interpreted by radiologist and people want to know whether machine can interpret or assist radiologist in reading these images. So that's the goal of this project. The first setp of the project follows other nice project published on the Github. But we hope to get some advances based on other people's work.
In this post, I will build a convulutional neural network, train it, and detect lung nodules. 


###Downloading Data

At first, I use data from the Lung Image Database Consortium and Infectious Disease Research Institute[(LIDC/IDRI) data base]{https://wiki.cancerimagingarchive.net/display/Public/LIDC-IDRI} 
This data is 124GB and you can get the annotations and nodule size in some additional documentations, which are good labels when you build CNN. But I don't use this data because it is a little huge. 
I ended up using reformatted version in LUNA16, which is a lung nodule detection challenge in 2016. Their website is: https://luna16.grand-challenge.org/Home/ 
The challenge is stoped but the data they use and the results are avaliable. The database they use is public avaliable LIDC/IDRI database.
In total, 888 CT scans are included. The data structured as follows:

    subset0.zip to subset9.zip: 10 zip files which contain all CT images
    
    candidates_V2.csv: csv file that contains the candidate locations for nodule and the calss 0 is for non-nodule while class 1 is for    nodule. In this file, 1351 nodule are labeled but the total candidates is 
    
You can download data from: https://drive.google.com/drive/folders/0Bz-jINrxV740SWE1UjR4RXFKRm8

###Creating Image Database

The images were formatted as .mhd and .raw files. The header data is contained in .mhd files and multidimensional image data is stored in .raw files. You have two methods to view the image. I use Paraview to view 3-D image. You can download Paraview from: (https://www.paraview.org/download/)
When you create Image Database, you have to read .mhd file by SimpleITK package. By the way, you have to put all mhd file and corresponding raw file in 10 subset to one file so the computer can read them one by one. I use SimpleITK to read mhd file. You can find the code in read_mhd_image function in create_images.py . Then I read csv file which contains candidates location for nodule. You should know the coordinate in this file is world coords but if you want to use image data, you have to convrt word coords to voxel coords. Finally, you can extract image with size of 50*50 according to coordinates in candidates.csv file. Then you can save these images.
