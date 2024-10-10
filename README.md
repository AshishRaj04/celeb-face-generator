# Celeb Face Generation using Variational Autoencoders (VARs)
---
In this project I have implemented the Variational Autoencoder models  to generate faces of celebrities. The model is trained on a dataset of celebrity faces and uses a combination 
encoder and decoder architecture to learn the distribution of the data and generate new faces.

[actual_vs_generated_image](saved-images\actual_vs_generated.png)

# Losses
---
* Total Loss - 72.2021
* Reconstrution Loss - 53.5756
* KL Loss - 18.7731

The total loss is the sum of the reconstruction loss and the KL divergence loss. The reconstruction loss is  the mean squared error between the input image and the reconstructed image. The KL divergence loss is the KL  divergence between the mean and log variance of the latent space and the prior distribution.

# Data 
---
The dataset used for this project is the CelebA dataset which contains 202,599 images of  celebrities. 
But for the sake of finishing this project on time I have to train the model with only 2563 image files due to very high computational cost .

#  Model Architecture
---
## Encoder Model 
Model: "encoder"
__________________________________________________________________________________________________
 Layer (type)                Output Shape                 Param #   Connected to                  
==================================================================================================
 encoder_input (InputLayer)  [(None, 128, 128, 3)]        0         []                            
                                                                                                  
 conv2d (Conv2D)             (None, 64, 64, 128)          3584      ['encoder_input[0][0]']       
                                                                                                  
 batch_normalization (Batch  (None, 64, 64, 128)          512       ['conv2d[0][0]']              
 Normalization)                                                                                   
                                                                                                  
 leaky_re_lu (LeakyReLU)     (None, 64, 64, 128)          0         ['batch_normalization[0][0]'] 
                                                                                                  
 conv2d_1 (Conv2D)           (None, 32, 32, 128)          147584    ['leaky_re_lu[0][0]']         
                                                                                                  
 batch_normalization_1 (Bat  (None, 32, 32, 128)          512       ['conv2d_1[0][0]']            
 chNormalization)                                                                                 
                                                                                                  
 leaky_re_lu_1 (LeakyReLU)   (None, 32, 32, 128)          0         ['batch_normalization_1[0][0]'
                                                                    ]                             
                                                                                                  
 conv2d_2 (Conv2D)           (None, 16, 16, 128)          147584    ['leaky_re_lu_1[0][0]']       
                                                                                                  
 batch_normalization_2 (Bat  (None, 16, 16, 128)          512       ['conv2d_2[0][0]']            
 chNormalization)                                                                                 
...
Total params: 3725584 (14.21 MB)
Trainable params: 3724560 (14.21 MB)
Non-trainable params: 1024 (4.00 KB)

## Decoder Model

Model: "decoder"
_________________________________________________________________
 Layer (type)                Output Shape              Param #   
=================================================================
 decoder_input (InputLayer)  [(None, 200)]             0         
                                                                 
 dense (Dense)               (None, 8192)              1646592   
                                                                 
 batch_normalization_4 (Bat  (None, 8192)              32768     
 chNormalization)                                                
                                                                 
 leaky_re_lu_4 (LeakyReLU)   (None, 8192)              0         
                                                                 
 reshape (Reshape)           (None, 8, 8, 128)         0         
                                                                 
 conv2d_transpose (Conv2DTr  (None, 16, 16, 128)       147584    
 anspose)                                                        
                                                                 
 batch_normalization_5 (Bat  (None, 16, 16, 128)       512       
 chNormalization)                                                
                                                                 
 leaky_re_lu_5 (LeakyReLU)   (None, 16, 16, 128)       0         
                                                                 
 conv2d_transpose_1 (Conv2D  (None, 32, 32, 128)       147584    
 Transpose)                                                      
...
Total params: 2275203 (8.68 MB)
Trainable params: 2257795 (8.61 MB)
Non-trainable params: 17408 (68.00 KB)
