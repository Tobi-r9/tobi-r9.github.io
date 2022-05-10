## Video Prediction with Diffusion models

You can use the [editor on GitHub](https://github.com/Tobi-r9/tobi-r9.github.io/edit/main/README.md) to maintain and preview the content for your website in Markdown files.
In this post we present a conditionally trained Video Diffusion Model which is able to succeed at several tasks, such as video generation, video prediction or inpainting. To adapt the Diffusion model from https://github.com/openai/improved-diffusion for Videos, we use 3D Convolutions. 

### Training
when training Video Diffusion models unconditionally, the generation works very well. However, conditional generation, by conditioning each diffusion step on some frames, does not create harmonic Videos. To overcome this we experimented with autoregressive resampling, predicting frame by frame and sample every step several times. This does help to some degree, but details are still not harmonized between the conditioned and predicted frames and increasing the resampling steps becomes unfeasible at some point. 
Unconditionally trained model on Video prediction conditioned on one frame  
![](bair_samples/unconditional_training/cond_0_8.png)  &rarr; ![](bair_samples/unconditional_training/seq_8.gif)  

Alternatively we propose to train the model conditionally. During training, we choose k random frames (where k is also randomly chosen each training step) which we do not diffuse. 
### Experiments on Bair

We train on the Bair dataset with 20 frames and each step we do not diffuse up to 4 random frames. First we show the results of the typicall Bair prediction protocoll (i.e. conditioning on one frame and predicting the next 15). This training technique works extremly well for prediction (we achieve an FVD of 90). However, we can still see, that the lightning is not always harmonized.  
![](bair_samples/conditional_training/prediction/cond_0_0.png) ![](bair_samples/conditional_training/prediction/cond_0_1.png) ![](bair_samples/conditional_training/prediction/cond_0_2.png) ![](bair_samples/conditional_training/prediction/cond_0_3.png) ![](bair_samples/conditional_training/prediction/cond_0_4.png) ![](bair_samples/conditional_training/prediction/cond_0_5.png) ![](bair_samples/conditional_training/prediction/cond_0_6.png) ![](bair_samples/conditional_training/prediction/cond_0_7.png) ![](bair_samples/conditional_training/prediction/cond_0_8.png) ![](bair_samples/conditional_training/prediction/cond_0_9.png) ![](bair_samples/conditional_training/prediction/cond_0_10.png) ![](bair_samples/conditional_training/prediction/cond_0_11.png) ![](bair_samples/conditional_training/prediction/cond_0_12.png) ![](bair_samples/conditional_training/prediction/cond_0_13.png) 
<p align="center">
    &#11015
</p>  

![](bair_samples/conditional_training/prediction/seq_0.gif) ![](bair_samples/conditional_training/prediction/seq_1.gif) ![](bair_samples/conditional_training/prediction/seq_2.gif) ![](bair_samples/conditional_training/prediction/seq_3.gif) ![](bair_samples/conditional_training/prediction/seq_4.gif) ![](bair_samples/conditional_training/prediction/seq_5.gif) ![](bair_samples/conditional_training/prediction/seq_6.gif) ![](bair_samples/conditional_training/prediction/seq_7.gif) ![](bair_samples/conditional_training/prediction/seq_8.gif) ![](bair_samples/conditional_training/prediction/seq_9.gif) ![](bair_samples/conditional_training/prediction/seq_10.gif) ![](bair_samples/conditional_training/prediction/seq_11.gif) ![](bair_samples/conditional_training/prediction/seq_12.gif) ![](bair_samples/conditional_training/prediction/seq_13.gif)

As the frames we condition on during training were chosen randomly, we can use the same model also for filling and generation.


