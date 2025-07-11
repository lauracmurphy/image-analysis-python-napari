---
title: Reference
---
## Primer on the Basics of Digital Images
### Pixels and Intensity  
Microscopy images are made up of pixels arranged in a grid. Each pixel stores a numerical value representing how bright that part of the image is, often referred to as the intensity. In most images, higher values mean brighter areas. These values are the foundation for all image-based measurements.

### Bit Depth  
Bit depth determines the range of intensity values that can be stored per pixel. An 8-bit image stores values from 0 to 255, while a 16-bit image allows values from 0 to 65,535. Higher bit depth enables better representation of subtle brightness differences, which is important when imaging faint or low-contrast structures.

### Image Dimensions  
Microscopy data often has more than two dimensions. In addition to spatial (x, y), you may also have:
- **z-stacks** (depth),
- **Time series** (t),
- **Multiple channels** (c).

This results in 3D, 4D, or even 5D images. Tools like Napari are built to work with n-dimensional image data.

### Channels  
Each channel represents a different signal or fluorophore, captured using specific excitation and emission settings (e.g. DAPI for nuclei or GFP-tagged proteins). These are usually stored as separate greyscale images and can be visualised together as composite images. Different channels are often analysed separately, depending on what they label.

### Brightness and Contrast  
Brightness and contrast settings determine how intensity values are mapped to your screen. You usually set a display minimum and maximum; for a linear greyscale lookup table, intensities below the minimum will appear black, those above the maximum will appear white, and values in between are scaled accordingly. These adjustments affect only the display, making structures appear brighter or increasing contrast. The underlying data is not affected.

### File Formats  
Microscopy images come in a range of formats:
- **Open formats** such as `.tif` (TIFF) are commonly used and broadly supported by analysis tools.
- **Proprietary formats** such as `.nd2`, `.czi`, and `.lif` are produced by specific microscope systems and often contain embedded metadata.
When exporting images for analysis, use formats that preserve full bit depth and metadata.

### Metadata  
Metadata is "data about data": it describes how to interpret the intensity grid. This includes pixel size (e.g. microns per pixel), z-step size, channel names, and microscope settings such as exposure time or objective lens. Metadata is essential for accurate measurements and reproducibility.

### Noise and Convolution  
All microscopy images contain **noise**: random fluctuations in pixel values that do not reflect the actual structure of the sample. Common sources include:
- **Shot noise** from the light detection process
- **Electronic noise** from the detector
- **Background autofluorescence** from the sample or mounting medium

**Convolution** in microscopy refers to how light from a single point in the sample spreads into a shape called the **point spread function (PSF)**, due to diffraction and optical limitations. This blurs the image and limits resolution. Many image processing steps aim to reverse or compensate for the effects of both convolution and noise.

### Filters  
Filters are used to reduce noise, enhance contrast, or correct illumination. Common examples include:
- **Gaussian blur**: smooths the image by averaging nearby pixels
- **Median filter**: removes speckle noise while preserving edges
- **Background subtraction**: removes uneven illumination using techniques such as rolling ball or difference of Gaussians

These filters can improve the performance of downstream analysis such as segmentation.

### Segmentation  
Segmentation is the process of identifying and outlining objects of interest (e.g. nuclei, cells, vesicles). It is a key step in quantitative image analysis. Approaches include:
- **Thresholding**: the process of deciding which pixels belong to the object or background based on their intensity  
- **Binarisation**: the result of thresholding; this converts the image into two values (typically 0 and 1), where one represents the object and the other the background  
- **Watershed**: splits touching objects based on shape or topography  
- **Semantic segmentation**: labels each pixel according to class (e.g. cell vs background)  
- **Instance segmentation**: detects and labels each object individually  
- **Deep learning-based tools**: [Cellpose](https://www.cellpose.org/), [StarDist](https://github.com/stardist/stardist), and [Instanseg](https://github.com/instanseg/instanseg) use pre-trained neural networks to perform instance segmentation. These tools can often give good results on complex or low-contrast images that are difficult to segment using traditional image processing methods.
  
## Python syntax primer

As this is a course on image analysis, some prior knowledge of Python syntax is assumed.
This reference provides a summary of the language constructs used in the examples and
exercises of this course.

### Variables

This is how you can store data to retrieve later:

```python
# assigning the integer 1 to the variable `a`, and the decimal 0.4 to
# the variable `b`
a = 1
b = 0.4

# we can perform arithmetic on numbers
c = a + 4

# even reassign a variable based on its previous value
b = b * 2

# strings/text can be specified with single quotes or double quotes
some_string = 'a b c d e'

# we can still use the `+` operator on strings, except instead this
# will concatenate them together
some_other_string = some_string + 'f g h i'

# Python also has the boolean values True and False
one_is_greater_than_zero = True
one_is_an_even_number = False
```

### Functions

These may be built into base Python, the standard library, extra installed packages, or ones that you've made
yourself. A function is always run with brackets.

```python
# show something on the console
x = 2
print(x)

# you don't have to create a variable first - you can just print a value directly
print('abc')
print(2)

# multiple arguments are separated with commas
print(1, 2, 3)

# some functions are written to take named arguments - check the function's documentation
# to see what arguments you can give it
print(1, 2, 3, sep='-')

# we still need brackets to run the function, even if they're empty
credits()

# the number 1 and the string '1' are not the same - Python has function for converting
# or 'casting' values to certain data types
string_1 = str(1)     # str -> cast to string
integer_4 = int(4.1)  # int -> cast to integer
float_3_point_0 = float(3)  # float -> cast to decimal
```

### Importing packages

Python comes with a lot of extra functionality that it not loaded by default. Some of these may be pre-installed (i.e. they are
part of the Python [standard library](https://docs.python.org/3/library/index.html)), or they may need to be installed with `pip`.

```python
# load the entire package - access its functions with dot notation
import skimage
image = skimage.io.imread('some_image.tif')

# some components inside packages are not functions, but regular
# strings, numbers, etc. - we still access them with dot notation but
# do not need `()` brackets to use them
import sys
print(sys.executable)

# import just the bits we need
from skimage.io import imread
image = imread('some_image.tif')

# rename the package as you're importing it
import matplotlib.pyplot as plt
plt.imshow(image)
```

### Lists

Python can use these to store many pieces of information together:

```python
# use square brackets to define a list, and separate the items with commas
some_list = ['a', 'b', 'c', 'd', 'e']

# access individual items with square brackets - note that Python counts from 0
print(some_list[0])
print(some_list[3])

# access a subset (slice) of a list with square brackets and colons - this will
# start at position 1 and go up to, but not including, position 3
print(some_list[1:3])

# negative numbers will count from the end of the list rather than the start
print(some_list[2:-1])

# leaving out the first number is equivalent to starting at position 0 (i.e. the
# start), and leaving out the second number is equivalent to ending at position -1
# (i.e. the end)
print(some_list[:3])
print(some_list[1:])

# leaving out both numbers will just slice the whole list
print(some_list[:])

# slicing and indexing also works with strings
some_string = 'abcdefgh'
print(some_string[2:5])

# images are designed to be indexed in multiple dimensions at once - do this
# by specifying multiple indexes/slices, separated by commas. Here we load an
# image and access all of dimension 1, positions 100-200 of dimension 2, and
# just position 2 of dimension 3
from skimage.io import imread
image = imread('some_image.tif')
print(image[:, 100:200, 2])
```

### Dictionaries

These store many named pieces of information together as key-value pairs:

```python
# use curly brackets to define a dictionary. Separate the key from the value
# with a colon, and separate key-value pairs from each other with commas
chromosome_counts = {'human': 46, 'wheat': 42, 'fruit fly': 8, 'zebrafish': 25}

# access individual values with square brackets
print(chromosome_counts['fruit fly'])
```

### Loops

This is how we can perform some actions on many pieces of information, one at a time:

```python
# first we need something to loop over
colours = ['orange', 'red', 'blue', 'green', 'yellow', 'purple']

# go through each item the `colours` list, one at a time. The item
# that we're currently processing will be called `colour`
for colour in colours:
    # the code inside the loop is indented with spaces or tabs - it doesn't
    # matter which one or how many, as long as you're consistent
    print('doing something with: ' + colour)

# we're no longer indented, so we're now outside the loop
print('done')

# this will do the same thing as the loop above, but with much more
# typing and repetition
print('doing something with: ' + 'orange')
print('doing something with: ' + 'red')
print('doing something with: ' + 'blue')
print('doing something with: ' + 'green')
print('doing something with: ' + 'yellow')
print('doing something with: ' + 'purple')
```

### Conditional statements

Python can execute blocks of code only when certain conditions are met:

```python
# use the keyword `if`, followed by a boolean expression. Common mathematical
# operators can be used in Python, including ==, !=, >, <, >=, <=
if 1 < 2:
    # 1 is less than 2, so this indented code will run
    print('1 is less than 2')

if 1 + 2 == 5:
    # 1 + 2 is not 5, so this will not run
    print('1 + 2 is 5')

# we can use `else` to provide some code to fall back on if the condition
# is not met
if 1 + 2 == 5:
    print('1 + 2 is 5')
else:
    print('1 + 2 is not 5')

# use `elif` to specify multiple possible courses of action - only the first one to
# be satisfied will be executed

# let's check how large each number in a list is
values = [5, 0, 2, 150, -1]

for val in values:
    if val > 100:
        print(str(val) + ' is greater than 100')

    elif val > 4:
        print(str(val) + 'is greater than 4')

    elif val >= 0:
        print(str(val) + ' is greater than or equal to 0')

    else:
        print(str(val) + ' is less than 0')
```