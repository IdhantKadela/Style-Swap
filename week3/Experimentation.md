# Problems Faced:
- A major change comes when I originally designed the model it created a latent vector of dimesion 1024 and then convolving it would 10^3 times more parameters than to just using latent vector of dimension 100. So training more number of parameters would require still larger dataset, hence did two changes to make it **computabily faster and to make it properly trainable** within the limit of given dataset:
1. Changing *latent dimension from 1024 to 100*
2. Taking images to *at max 512 channels rather than 1024* during the DC layers.
- I faced a problem of importing data, I had to use Image.open('path').convert('RBG'), otherwise it was giving me grayscaled image.
- I thought that I can train on around the same number of images as in UNet, but GAN require higher number of samples to be trained since it is generated from random noise afterall.
- To remove any fullyconnected layer, I replaced the linear layer in the end of discriminator with a convolution of kernel size 4 and stride 2