### Cropping
This was easy and after some rough tries I found out the perfect square that contains only the coloured mario in frame, which was **9% to 85% height** (from top) and **10% to 45% width** (from left). I have added extra 12 pixels in width to make it equal to the number of pixels in height just to make sure that performing convolutions is _smooth_.</br>
I defined some basic functions which were useful further.
### Axial Edge Detectors
The basic idea anyone would think of to detect edges is detecting horizontal and vertical edges. I wrote 3x3 matrices with entries forming a _gradient_ in a particular direction. The direction of this _gradient_ tells us which _edge_ is that particular filter going to detect. For example a gradient of values (1 -> 0 -> -1) from left column to right column will detect left vertical edges and similar gradient from top row to bottom row will detect upper horizontal edges.<br>
### The Combination
After analysing these four maps in the different channels, it clicked to combine these into a single map. I choose to summing them up since I've already applied ReLU, the mess of negative numbers was gone already. RMS value can also be a good choice to work with but in the small interval of 0 to 1 (after normalisation) it will not make some noticeable change.
### Thresholding
I noticed that the edges were very thick and blurry. Since it was mainly due to less brighter _leaks_ around the edges. I tried thresholding my image such that all pixels which are less bright than 15% of most bright pixel should truncate to zero (absolute black). This sort of _cleaned_ the edges.
### Sobel-Feldman & Robert Operators
I used Sobel-Feldman and Robert operators by defining them explicitly for different directions and then combining via root of sum of sqaured values.
- Results of Sobel-Feldman was close to axial edge detection's combination. Aa slight difference was that Sobel map was less noisy than the usual one.
- A more siginificant fact was that the Robert filter combined edges in the diagonal direction rather than axial, which made it different and very well-defined.
### Gaussian Blur
Since the original Mario image was not really noisy, I did not do gaussian blurring in the original Mario pic. But since the code must be optimised, I added Gaussian Blur on the user input and the kernel was based on the following formula that I found on Wikipedia:
Here the kernel is of size _(2k + 1) x (2k + 1)_ and &#963 is the standard deviation.
<p align="center">
<img src="https://wikimedia.org/api/rest_v1/media/math/render/svg/4a36d7f727beeaff58352d671bb41a3aca9f44d6" />
</p>