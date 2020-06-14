# Feature detection and matching

# Classes of features

1. [Points and patches:](#points)
  - specific locations in images eg: mountain peaks, building corners, etc.
  - these kinds of localized feature are called keypoint features/ interest 
    points/ corners
  - appearance of patches of pixels surrounding the point location

2. [Edges](#edges)
  - eg: profile of mountains against the sky
  - can be matched based on their orientation and local appearance (edge profiles)
  - good indicatiors of object boundaries and occlusion events in image sequences.
  - types: longer curves and straight line segments

> Feature detection
> Eg of panorama: match portions of image

<a name="pjoints"></a>

# Points and patches

- Point features can be used to find a sparse set of corresponding locations in 
  different images
- prerequisite for computing a denser set of correspondences using stereo matching
- correspondences can also be used to align different images
- used to perform object recognition and category recognition
- 2 methods for finding feature points and their correspondences:
    1. find features in one image that can be accurately tracked using a local 
    search technique, such as correlation or least squares. 
    Suitable when images taken from nearby viewpoints or rapid succession (video)
    2. independently detect features in all the images under construction and 
    then match features based on their local appearnance.
    Suitable when a large amount of motion or appearance change is expected eg. 
    stitching panoramas

4 stages of keypoint detection and matching pipeline:

1. Feature detection (extraction) stage: searhed for locations that are likely 
to match well in other images
2. Feature description stage: define region around detected keypoint locations,
extract and normalize the region content and
convert into compact and stable (invariant) descriptor
3. Feature matching stage:  efficiently searches for likely matching candidates
in other images.
4. Feature tracking stage: is an alternative to the third stage that only 
searches a small neighborhood around each detected feature and is therefore more
suitable for video processing.

Example: David Lowe's 2004 paper (SIFT)

## 1. Feature Detectors:

Motivation for using local features:
- Global features have major limitations
- Increased robustness to
  - occlusions
  - articulation
  - intra-category variations

Find image locations where we can reliably find correspondences with other 
images, i.e., what are good features to track 

We are interested to find loctions such that the minimum change caused by
shifting the window in any direction is large.

Patches with large contrast changes are easier to localize.

The simplest possible matching criterion for comparing two image patches is the 
weighted summed square difference.

$$
E_{WSSD}(\vec \mu) = \sum_{i} w(\vec{x_{i}})[I_1(\vec{x_i}+\vec{\mu}) - I_0(\vec{x_i})]^2,
$$

where, 
$I_0$ and $I_1$ are the two images being compared,

$\vec{\mu} = (u,v)$ is the displacement vector,

$w(\vec x)$ is a spatially varying weighting function,

the summation $i$ is over all the pixels in the patch.

Since we don't know which other image locations the feature will end up being
matched against, we can only cimpute how stable this metric is with respect
to samll variations in position, $\Delta \vec u$ by comparing an image patch
against itself, which is also called *auto-correlation function or surface*


$$
E_{AC}(\Delta \vec \mu) = \sum_{i} w(\vec{x_{i}})[I_0(\vec{x_i}+\Delta \vec{\mu}) - I_0(\vec{x_i})]^2,
$$


### Forstner-Harris (Harris Corner):

Forstner (1986) and Harris and Stephens (1988) were the first to propose using 
local maxima in rotationally invariant scalar measures derived from the 
auto-correlation matrix to locate keypoints for the purpose of sparse feature
matching.


Harris and Stephens (1988) proposed a simpler quantity that can be used to find 
keypoints which is:

$$
\det(A) - \alpha \hspace{2pt}\mathrm{trace}(A)^2 = \lambda_0 \lambda_1 - \alpha (\lambda_0 + \lambda_1)^2
$$

where,

$A = w \nabla I \nabla I^T$ is the auto correlation matrix

Using Taylor's series expansion of the image function 
$I_0(\vec{x_i} + \Delta \vec \mu) \approx I_0(\vec{x_i})$

