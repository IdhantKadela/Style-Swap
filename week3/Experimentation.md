# Problems Faced:
- I faced a problem of importing data, I had to use Image.open('path').convert('RBG'), otherwise it was giving me grayscaled image.
- I thought that I can train on around the same number of images as in UNet, but GAN require higher number of samples to be trained since it is generated from random noise afterall.