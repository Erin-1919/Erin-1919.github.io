---
title: "GIS Basics: Digital Image Processing"
layout: post
---

>> Good to begin well, better to end well.
>> 
>> -- June K. Robinson

I set up a [mind map](https://drive.google.com/file/d/11nuzFqrosP19N0ncjL1-rthJ9jmMqWtB/view?usp=sharing) and wrote detailed [documentation](https://drive.google.com/file/d/1hn2AbcAKBWCZrBU3ng4gLPpaCu2OhDs3/view?usp=sharing) to help myself organize, understand, and memorize knowledge and concepts regarding GIS when preparing for my PhD candidacy exam. 

This is the fifth part of the doc: **Digital Image Processing**.

The content is largely the notes I made after watching this [video list](https://www.youtube.com/playlist?list=PLuh62Q4Sv7BUf60vkjePfcOQc8sHxmnDX).

## Spatial filters
A convolution is to put a kernel (namely filter, mask) on the image, calculate the products of each corresponding element, sum them up, and assign this new value to the center pixel of the kernel on the image. The main task is then to define the appropriate kernels to produce different desired results. There are generally two spatial filters or kernels: smoothing filter (low pass filter) and sharpening filter (high pass filter). 
 
### Smoothing filter
Moving average filter is the simplest smoothing filter, which takes the average of the pixel values within the kernel and assigns it to the central pixel. Gaussian filter is to assign the Gaussian weighted average within the kernel to the central pixel. Both the moving average filter and Gaussian filter is good for removing the Gaussian noise in the image. The median average filter is a non-linear filter, assigning the median value in the neighborhood to the central pixel. The median averaging is good for removing the impulse noise (i.e., salt and pepper noise) in the image. The bilateral filter is used to remove the noise in an image while keeping the edges sharp. Bilateral filtering applies two Gaussian filters, one for spatial smoothing, and one for identifying the pixel differences. The Gaussian function of intensity difference makes sure that only those pixels with similar intensities to the central pixel are considered for blurring and leave the others with large intensity variation (edge) unchanged.

### Sharpening filter
The basic idea of the sharpening filter is to find the kernels that react strongly to the regions with image differencing (edges). This can be dependent on either the first derivative or gradient of the image or the second derivative of the image. Around the edges, the first derivative will experience an increase of the value, and the second derivative will experience the sign changes. The approximations of Laplacian are good examples of the sharpening filter, which is the second partial derivative of the image in both directions. Laplacian derivatives highlight the regions in which there is a rapid intensity change using a discrete convolution kernel that approximates the second derivatives of the image in the definition of the Laplacian. To enhance an image, one can add a multiple edge map to the original map but may come across the problem that the noise is also sharpened. Unsharp masking is developed to solve this problem by adding a tunable fraction of the edges back in for a subtle effect. So, with unsharp masking, one can sharpen the edges of the elements without increasing the noise or blemish.

## Edge detection
Edge detection is fundamentally related to the gradient of the image. Gradient direction is always perpendicular to edges. The magnitude and the angle of the gradient can be calculated by the first partial derivatives of the image in two directions. Four methods of edge detection are introduced here: Sobel edge detection, Laplacian-of-Gaussian filter, difference-of-Gaussian filter, and Canny operator. 
 
### Sobel edge detection
Sobel operator is a discrete differential operator that computes an approximation of the gradient of an image intensity. The orientation of a Sobel operator can be set as horizontal, vertical, or other degrees. It can be used to find edges in one direction while smooth the image in another direction. However, a problem with the Sobel operator is that it can only find the edges at the same scale as the kernel window. 
 
### Laplacian-of-Gaussian
Laplacian-of-Gaussian operator (i.e., LoG operator), also known as Marr-Hildreth filter or Mexican hat filter is an edge detector that can be tuned for edges at different scales. Big operators can detect blurry edges at a large scale, and small operators can detect fine edges at a small scale. It is essentially a two-step filer that smooths the image by Gaussian filter before applying the Laplacian filter to enhance the edges. Specifically, the Gaussian filter smoothens the image down to a certain scale and the Laplacian filter finds the edges at the scale by looking for zero-crossings of LoG operators. This LoG kernel is convolved with a grayscale input image to detect the zero-crossings of the second derivative.
 
### Difference-of-Gaussian
The difference-of-Gaussian operator is essentially a spatial band-pass filter, which is an edge detector that generates the differences of two separable Gaussian convolutions. 
 
### Canny operator
The canny operator is a multi-step filter that generally results in cleaner edges. The first step is to smooth the image with a Gaussian filter. The second step is to compute the magnitude and angle of the gradient which is perpendicular to the edge. The third step is applying the non-maximum suppression to the gradient's magnitude to obtain a new gradient image. The principle is to compare the magnitude within its neighborhood in the direction of the gradient, then keep the raw value only if it is the local maximum and suppress to zero if not. The final step is to detect and link the edges. In this step, users are to define two thresholds, a higher one and a lower one. Edge pixels greater than the higher threshold are classified as strong edges and are kept in the final edge set. Those pixels between two thresholds are classified as weak edges, and only those weak edges adjacent to (one pixel) to the strong edges will be kept in the final edge set. 

## Edge linking
Edge linking is based on the edge detection operation introduced above, usually starting with a binary image where 1 represents an edge pixel and 0 represents a non-edge pixel. Here I focus on a few operations: trace long edges, Moore's boundary following along with the chain coding methods, polygon fitting, and straight-line fitting. 
 
### Trace long edges
To trace a potentially long edge, one starts with an edge pixel and corresponding magnitude and angle. For each edge pixel, link it to the other edge pixel in its local neighborhood which has a similar magnitude and angle. Two thresholds regarding magnitude and angle should be decided in advance. The output is the traced long edge.
 
### Moore's boundary following 
Moore's boundary following algorithm aims to link or order the edge points around a closed contour. It starts with a starting edge point which is normally the upper-left edge pixel. Then from the left pixel of the starting point, examine its eight neighbors clockwise until finding the first edge pixel. Move to the newly found edge pixel, start from the previous non-edge pixel, and clockwise examine its eight neighbors. Repeat the steps until going back to the initial starting point. The ordered list of all found edge pixels is the boundary. 
 
### Chain coding methods
To encode the determined boundary which is a list of edge pixels, one defines eight directions by eight integers. Start from one pixel and go clockwise, the direction of each movement is recorded. This is called the absolute direction encoding. However, the final chain code varies depending on the starting point and is not practical for matching shapes with different orientations. To solve this problem, one can reorder the chain codes with absolute directions with the minimum magnitude integer as the start point or can apply the relative direction encoding which encodes the difference of directions at each movement.
 
### Polygon fitting
After we get the ordered edge pixels, one can fit a polygon based on the boundary. The algorithm is similar to the Douglas-Peucker algorithm which connects points only if the distance between a point and the line segment is greater than the threshold. 
 
### Straight line fitting
Hough transformation is used in fitting multiple straight lines in an image at the same time. The main idea is that all lines passing one point (x,y) on the (x,y) plane can be represented by a curve on the (ρ,θ) plane. Two curves representing lines passing point (x1,y1) and point (x2,y2) on the (x,y) plane intersect at the point (ρ1,θ1) on the (ρ,θ) plane, meaning that the line passes the points (x1,y1) and (x2,y2) on the (x,y) plane. The specific steps are: 1) detect edge pixels and generate the binary image, 2) decide on the subdivision of (ρ,θ) plane, 3) for each edge pixel pair, increment the (ρ,θ) cell by 1, 4) after examining all pairs, look for the (ρ,θ) cell with the maximum counts, and 5) select the highest peaks and map the corresponding (ρ,θ) in the (x,y) plane. 

## Thresholding
Thresholding is a common tool for image segmentation. Global thresholding aims to define one threshold on the entire image and distinguish the foreground and background. Otsu's algorithm is one approach to determine the best global threshold which is to maximize the between-class variance. The generalization form of the Otsu's algorithm is to find (k-1) global thresholds to separate k classes. There are occasions when Otsu fails, such as there are no strong peaks in the histogram, or the object is too small compared to the background. The possible solutions include doing a low pass filter before the Otsu's algorithm or only consider the pixels near edges when computing thresholds. On the contrary to the global thresholding, variable thresholding or adaptive thresholding applies different local thresholds on the image especially for those that have various illumination. The block-wise thresholding is to apply a specified function such as the Otsu's algorithm to each block of an image, and one needs to define a proper block size beforehand. The pixel-wise thresholding is to build a neighborhood for each pixel and compute the mean and standard deviation within this neighborhood. Then different models or criteria can be used to determine each pixel compared to the neighborhood mean and deviation. The thresholding can also be used on combined color channels or a distance from a chosen color. This process is called color thresholding. Other machine learning methods like k-means clustering can be used in the image segmentation as well, and this is introduced in the spatial data mining section. 
 
## Image segmentation
Here we talk a bit more about image segmentation, covering methods like basic region growing, the region split and merge, clustering and super-pixels, and graph cut segmentation. 

### Basic region growing
The basic region growing algorithm starts from a binary image generated by thresholding. The binary image is called a seed image. Then one reduces the seed connected block down to single points. After that, set the neighboring pixel of the center point each time if a pre-defined condition is met. The condition can be, for example, the pixel is 8-connected to the seed point and their intensity difference is less than a threshold. 
 
### Region split and merge
Region split and merge are to specify a condition and subdivide the regions that do not satisfy the rule. This process is similar to the quadtree construction process. 
 
### Clustering and super-pixels
K-means clustering is a commonly used unsupervised algorithm that follows the steps: 1) specify an initial set of cluster centers which can be determined as the histogram peaks; 2) for each data point, assign it to the cluster whose center is closest to the point; 3) update the cluster centers with the average value of all points in this cluster, and 4) repeat steps 2 and 3 until convergence. 
 
A modification of the k-means cluster is to use super-pixels to substitute the real pixels in the clustering. The steps are as follows: 1) initialize super-pixel centers by sampling n locations on a regular grid; 2) for each cluster center compute the distance between each pixel and the center in a neighborhood of the center; 3) assign the pixel to the cluster if the distance is better than it was before; 4) update the cluster centers, and 5) repeat steps 2-4 until convergence. In this scenario, the distance is defined as the combination of color distance and spatial distance. 
 
### Graph cut segmentation
The graph cut segmentation is used to separate the foreground and background, especially for complex images. The initiation of the algorithm is to let each pixel connect to the foreground and background terminals. Then a cut is applied to the image to remove separates of foreground and background with a set of edges. To find out the best cut, one needs to assign a weight to each edge to find the min-cut.

## Morphological image processing
Morphological transformations are operations based on the image shape, normally performed on binary images. It needs two inputs: an original image and a structuring element or kernel which is a small pixel template that helps to produce the new image from the old one. Simple operations on sets of pixels include translation, reflection, and rotation.
 
### Erosion and dilation
Erosion and dilation are two basic operations in morphological processing, where erosion computes a set of points that the shifted structuring element fits fully inside of the original image, and dilation computes a set of points that the shifted structuring element has any overlap with the original image. Erosion is useful for removing small white noises in an image by eroding the boundaries of the foreground object. Dilation is the opposite of erosion and is useful in joining the broken parts of an object. 
 
### Opening and closing
The opening is a two-step process combining erosion and dilation, which is used to break down bridges and eliminate thin structures. Closing applies the opposite order where dilation is followed by erosion. Closing is useful in fusing narrow breaks and eliminating small holes.
 
### Top hat and black hat
The top hat produces the difference between the input image and the opening process, while the black hat produces the difference between the input image and the closing process. 
 
### Morphological gradient 
Morphological gradient produces the difference between the dilation and the erosion of an image, used to extract boundaries or outlines.
 
### Flood filling and watershed segmentation
Flood filling, also known as hole filling, is to keep on dilation as long as stays in the region. Watershed segmentation is an erosion process to remove thin lines and isolated dots and to leave gross details.
 
## Region description
There are a series of measurements to describe a region on an image, including perimeter, area, diameter, bounding box, compactness, circularity, centroid, and eccentricity of the best-fit-ellipse. Skeletonization is a process for reducing foreground regions in a binary image to its medial axis. The process can be done through either successive erosions or distance transformation. The distance transform is an operator that computes the gray level intensities of points inside foreground regions to show the distance to the closest boundary from each point. Based on the produced distance metric, the skeletons can be extracted. 
  
## Object detection
Object detection deals with detecting instances of semantic objects of a certain class in digital images and videos. Template matching and SIFT are commonly used in object detection. 

### Template matching
Template Matching is a method for searching the location of a template image in a larger image. The basic idea is to calculate the correlation coefficient between the template and the corresponding window area of the larger image and returns a grayscale image where each pixel denotes how much does the neighborhood of that pixel match with the template. If the correlation coefficient equals 1, then the template is exactly equal to or is a positive multiple of the image patch in the window. If the correlation coefficient equals -1, then the template has flipped intensities of the image patch. If the correlation coefficient equals 0, then no match is detected. A good template or feature normally have edge strength in two directions. SHI-Tomasi corner detection is used to find corners on a certain scale.
 
### SIFT
The scale-invariant feature transform or SIFT is a feature detection algorithm to detect and describe local features in images at various scales. It has five main stages: scale-space extreme detection, keypoint localization, orientation assignment, keypoint descriptor, and keypoint matching. The first step is to search over all scales and image locations by implementing a difference-of-Gaussian function to identify potential interest points that are invariant to scale and orientation. Then, at each candidate location, a detailed model is fit to determine location and scale, and key points are selected based on measures of their stability. One or more orientations are assigned to each keypoint location based on local image gradient directions. The local image gradients are then measured at the selected scale in the region around each key point. Finally, the key points between the two images are matched by identifying their nearest neighbors.

## Image restoration
Image restoration is an objective method to restore an image based on the way it was degraded. This is different from the subjective methods such as low pass filtering, median filtering, and unsharp masking. The typical noise existing in an image can be classified based on its histogram distribution: Gaussian noise like thermal and sensor noise, Rayleigh noise in range imaging, exponential noise in laser imaging, salt and pepper noise, or impulse noise caused by sharp and sudden disturbances in the image signal, and uniform noise. To determine a constant noise type, one can find a region that should be flat with constant intensity and plot the histogram of its intensity. A patch-based formulation or PDF can be fit to the histogram to determine the possible noise type. 
 
An adaptive filter can be applied to restore an image, which would change depending on the noise characteristics in the local window. To do this, a global variance of noise in the entire image needs to be estimated beforehand. If the global variance equals zero, then the restored intensity equals the original image; if the local variance is far greater than the global variance, then keep the restored intensity equal to the original image; if the local variance approximates the global variance, then assign the local mean to the restored intensity value. This can make sure that edges are kept when doing averaging.
 
Wiener filtering assumes that if noise is present in the system, then it is considered to be additive white Gaussian noise or AWGN. It is essentially a mean square error filtering and can remove image noise and restore blurred images at the same time.
 
## Image blending
The set of images with progressively lower resolutions are called image pyramids. For a Gaussian pyramid, a higher level is formed by removing consecutive rows and columns in the lower level of the image. Each pixel in a higher level is formed by the contribution from five pixels in the underlying level with Gaussian weight, and the area reduces to one-fourth of the original area. The same pattern continues as going upper in the pyramids. The Laplacian pyramid depends on the Gaussian pyramid. A level in Laplacian Pyramid is formed by the difference between that level in the Gaussian Pyramid and the expanded version of its upper level in the Gaussian Pyramid. Thus, Laplacian pyramid images are like edge images only presenting the detailed decomposition of edges. To restore the original image from the Laplacian pyramid, one needs to add back all the edges at different scales from the smallest image. Gaussian pyramids and Laplacian pyramids can be used in image composition or image blending. For example, to blend two images, one can compute the Gaussian pyramids and Laplacian pyramids, join the two images at each level of Laplacian Pyramids, and reconstruct the image by adding up to the final composite. 




