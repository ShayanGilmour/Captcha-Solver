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

### How does it work?
#### Training
Using Convolutional Neural Network, it learns each digit. (Only one digit)
#### Process
After a Captcha is given to the program, first it converts to to Black and White, then it reduces the noise of the Captcha by replacing the dim and pale pixels with complete white, and then, replacing the remaining dark pixels with complete black. Let's assume the left below is the Original Captcha; The program converts it to Black and white (The right below):
<p float="left">
  <img src="https://user-images.githubusercontent.com/12760574/130741012-7cf14226-0f60-4667-b633-7da8ea25c1d8.png" width="600" />
</p>

In the stage of reducing the noise, the factor that matters the most, is the definition of the “Pale Pixel” that is mentioned above. If we scale the brightness of a B/W pixel from 0 to 255, 0 being completely black and 255 being completely white, from what point to 255, a pixel is considered a pale pixel? After that, we’ll edit the picture in such a way that there are only back and white pixels (No gray pixels,) so each pixel is either completely back or completely white.
<p float="left">
  <img src="https://user-images.githubusercontent.com/12760574/130741219-baa37c07-20d4-4fd9-b84e-fb5bd82a0f29.png" width="600" />
</p>

Below are few more examples of this process being done on some other Captchas:
<p float="left">
  <img src="https://user-images.githubusercontent.com/12760574/130741758-ccf53df4-cfd3-4998-aebb-077db4843e98.png" width="600" />
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

<p float="left">
  <img src="https://user-images.githubusercontent.com/12760574/130742307-3344470f-c010-4ef7-8bd9-926b3bd427cb.png" width="600" />
</p>

So the program can easily find the positions of the digits, and
crops each digit individually:

<p float="left">
  <img src="https://user-images.githubusercontent.com/12760574/130743118-fb519a99-823e-4075-a05e-5383db81f91c.png" width="600" />
</p>

Now the program will resize each digit to the standard input size
of its Neural Network (which is 40×20) and give it to its CNN:
<p float="left">
  <img src="https://user-images.githubusercontent.com/12760574/130742795-981eb25c-f863-4da8-8b2d-c25654d20ed9.png" width="600" />
</p>
<p float="left">
  <img src="https://user-images.githubusercontent.com/12760574/130750931-4a7c4984-ec02-45e5-8c9b-aa26b27b2e99.png" width="300" />
  <img src="https://user-images.githubusercontent.com/12760574/130750953-31da61a0-ce5b-46be-8be2-140c7c813572.png" width="300" />
  <img src="https://user-images.githubusercontent.com/12760574/130750967-b94e66c6-4eaa-4352-9641-f907d95eabff.png" width="300" />
  <img src="https://user-images.githubusercontent.com/12760574/130750981-e9b359a0-8668-4843-8158-5ca7a39bec68.png" width="300" />
  <img src="https://user-images.githubusercontent.com/12760574/130750987-27f20d4d-ebc3-4e96-979a-2dba221a5c35.png" width="300" />
  <img src="https://user-images.githubusercontent.com/12760574/130750995-c560ff2a-bf66-4f48-b1a9-1d6ae9a2683b.png" width="300" />
</p>
