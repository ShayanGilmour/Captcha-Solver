# Captcha-Solver
A Convolutional Neural Network solving Captcha

### Dataset
To do this, this code first generates its own dataset. Using `claptcha` and a variety of fonts.
<p float="left">
  <img src="https://user-images.githubusercontent.com/12760574/130737658-69327e3d-facd-47e7-a050-336336e82c7e.png" width="600" />
</p>
Then using `claptcha`, we generate a dataset for each digit (and characters if you want,)
<p float="left">
  <img src="https://user-images.githubusercontent.com/12760574/130739503-be053555-7730-420a-97f7-09bbb0d7b135.png" width="600" />
</p>

You can see that `claptcha` inputs a arbitrary font, and the base font plays an important role. On left, there's the base font, and on the right, the corresponding distorted image created by claptcha:
<p float="left">
  <img src="https://user-images.githubusercontent.com/12760574/130739758-405ab90e-e1ae-4a58-a1d5-7f0b1ff44045.png" width="600" />
</p>

### Training
Using Convolutional Neural Network, it learns each digit. (Only one digit)

### How does it work?
After a Captcha is given to the program, first it converts to to Black and White, then it reduces the noise of the Captcha by replacing the dim and pale pixels with complete white, and then, replacing the remaining dark pixels with complete black. Let's assume the left below is the Original Captcha; The program converts it to Black and white (The right below):
<p float="left">
  <img src="https://user-images.githubusercontent.com/12760574/130741012-7cf14226-0f60-4667-b633-7da8ea25c1d8.png" width="600" />
</p>

In the stage of reducing the noise, the factor that matters the most, is the definition of the “Pale Pixel” that is mentioned above. If we scale the brightness of a B/W pixel from 0 to 255, 0 being completely black and 255 being completely white, from what point to 255, a pixel is considered a pale pixel? After that, we’ll edit the picture in such a way that there are only back and white pixels (No gray pixels,) so each pixel is either completely back or completely white.
<p float="left">
  <img src="https://user-images.githubusercontent.com/12760574/130741219-baa37c07-20d4-4fd9-b84e-fb5bd82a0f29.png" width="600" />
</p>

Below are few more examples of this process being done on some other Captchas:
![Screenshot from 2021-08-25 11-28-57](https://user-images.githubusercontent.com/12760574/130741758-ccf53df4-cfd3-4998-aebb-077db4843e98.png)

<p float="left">
  <img src="https://user-images.githubusercontent.com/12760574/130741219-baa37c07-20d4-4fd9-b84e-fb5bd82a0f29.png" width="600" />
</p>

### Cropping digits
After reducing the noise of the picture, the program will chop the image in a few slices(!) so that in each slice, there’s only one digit. How does the program do that? The program has 3 functions that calculate the density of black pixels in an area.
  function does this differently; For instance one function just
counts the number of black pixels in the given area and returns it,
while the other function will find the largest sub-rectangle that
all of its pixels are black, and returns the area of that rectanglesquared; The other function does something similar to this
function. Combining these three functions, we can find the areas
that the digits are placed; Then we can easily crop them. Consider
the first example, we’ll graph the combination of these density
function:
