# Semantic Segmentation
[Road Expample1]: ./images/um_000019.png
[Road Expample2]:./images/um_000020.png
[Road Expample3]:./images/um_000021.png
[Road Expample4]:./images/um_000022.png
[Road Expample5]:./images/um_000023.png

### Introduction
The goal of this project is to label the pixels of a road in images using a Fully Convolutional Network (FCN) as described in the paper(in classroom) [Fully Convolutional Networks for Semantic Segmentation](https://people.eecs.berkeley.edu/%7Ejonlong/long_shelhamer_fcn.pdf) by Jonathan Long, Evan Shelhamer, and Trevor Darrell from UC Berkeley. 

### Architecture

    layer_7_conv_1x1: conv2d(kernel_size=1, strides=1)
    layer_7_upsampled: conv2d_transpose(kernel_size=4 and strides=2)
    layer_4_conv_1x1: conv2d(kernel_size=1, strides=1)
    layer_4_upsampled: conv2d_transpose(kernel_size=4 and strides=2)
    layer_3_conv_1x1: conv2d(kernel_size=1, strides=1)
    layer_3_upsampled: conv2d_transpose(kernel_size=16 and strides=8)
    
Encoder part downsampling is done using conv2d() and decoder for upsampling conv2d_transpose() has been setup with a kernel initializer (tf.random_normal_initializer) and a kernel regularizer (tf.contrib.layers.l2_regularizer). Upsampling and downsampling are followed by skip connections using tf.add(). 

### Training on AWS EC2 Instance
The FCN has been trained on an Amazon Web Services (AWS) EC2 g2.2xlarge instance.

Created anaconda environment file environment.yml to setup the EC2 instance with python v3.5.2, tensorflow v1.4 and all dependencies

Prepare Anaconda environment:

     conda env create -f environment.yml


### Hyper-Parameters
Due to the limited storage the batch size was set to 2 and 20 epochs.

### Results
![Expample1][Road Expample1]
![Expample2][Road Expample2]
![Expample3][Road Expample3]
![Expample4][Road Expample4]
![Expample5][Road Expample5]



### Setup
##### GPU
`main.py` will check to make sure you are using GPU - if you don't have a GPU on your system, you can use AWS or another cloud computing platform.
##### Frameworks and Packages
Make sure you have the following is installed:
 - [Python 3](https://www.python.org/)
 - [TensorFlow](https://www.tensorflow.org/)
 - [NumPy](http://www.numpy.org/)
 - [SciPy](https://www.scipy.org/)
##### Dataset
Download the [Kitti Road dataset](http://www.cvlibs.net/datasets/kitti/eval_road.php) from [here](http://www.cvlibs.net/download.php?file=data_road.zip).  Extract the dataset in the `data` folder.  This will create the folder `data_road` with all the training a test images.

### Start
##### Implement
Implement the code in the `main.py` module indicated by the "TODO" comments.
The comments indicated with "OPTIONAL" tag are not required to complete.
##### Run
Run the following command to run the project:
```
python main.py
```
**Note** If running this in Jupyter Notebook system messages, such as those regarding test status, may appear in the terminal rather than the notebook.

### Submission
1. Ensure you've passed all the unit tests.
2. Ensure you pass all points on [the rubric](https://review.udacity.com/#!/rubrics/989/view).
3. Submit the following in a zip file.
 - `helper.py`
 - `main.py`
 - `project_tests.py`
 - Newest inference images from `runs` folder  (**all images from the most recent run**)
 
 ### Tips
- The link for the frozen `VGG16` model is hardcoded into `helper.py`.  The model can be found [here](https://s3-us-west-1.amazonaws.com/udacity-selfdrivingcar/vgg.zip)
- The model is not vanilla `VGG16`, but a fully convolutional version, which already contains the 1x1 convolutions to replace the fully connected layers. Please see this [forum post](https://discussions.udacity.com/t/here-is-some-advice-and-clarifications-about-the-semantic-segmentation-project/403100/8?u=subodh.malgonde) for more information.  A summary of additional points, follow. 
- The original FCN-8s was trained in stages. The authors later uploaded a version that was trained all at once to their GitHub repo.  The version in the GitHub repo has one important difference: The outputs of pooling layers 3 and 4 are scaled before they are fed into the 1x1 convolutions.  As a result, some students have found that the model learns much better with the scaling layers included. The model may not converge substantially faster, but may reach a higher IoU and accuracy. 
- When adding l2-regularization, setting a regularizer in the arguments of the `tf.layers` is not enough. Regularization loss terms must be manually added to your loss function. otherwise regularization is not implemented.
 
### Using GitHub and Creating Effective READMEs
If you are unfamiliar with GitHub , Udacity has a brief [GitHub tutorial](http://blog.udacity.com/2015/06/a-beginners-git-github-tutorial.html) to get you started. Udacity also provides a more detailed free [course on git and GitHub](https://www.udacity.com/course/how-to-use-git-and-github--ud775).

To learn about REAMDE files and Markdown, Udacity provides a free [course on READMEs](https://www.udacity.com/courses/ud777), as well. 

GitHub also provides a [tutorial](https://guides.github.com/features/mastering-markdown/) about creating Markdown files.
