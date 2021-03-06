# Generative Image Inpainting with Contextual Attention

[Paper](http://jhyu.me/resources/publications/yu2018-generative-inpainting-paper.pdf) | [arXiv](https://arxiv.org/abs/1801.07892) | [Project](http://jhyu.me/posts/2018/01/20/generative-inpainting.html) | [Demo](http://jhyu.me/posts/2018/01/20/generative-inpainting.html#post)



<img src="https://user-images.githubusercontent.com/22609465/35317673-845730e4-009d-11e8-920e-62ea0a25f776.png" width="425"/> <img src="https://user-images.githubusercontent.com/22609465/35317674-846418ea-009d-11e8-90c7-652e32cef798.png" width="425"/>

<img src="https://user-images.githubusercontent.com/22609465/35317678-848aa3fc-009d-11e8-84a5-01be01a31fc6.png" width="210"/> <img src="https://user-images.githubusercontent.com/22609465/35317679-8496ab84-009d-11e8-945c-e1f957b04288.png" width="210"/>
<img src="https://user-images.githubusercontent.com/22609465/35347783-c5e948fe-00fb-11e8-819c-8212d4edcfd3.png" width="210"/> <img src="https://user-images.githubusercontent.com/22609465/35347784-c5f4242c-00fb-11e8-8e46-5ad224e15096.png" width="210"/>

Example inpainting results of our method on images of natural scene (Places2), face (CelebA) and object (ImageNet). Missing regions are shown in white. In each pair, the left is input image and right is the direct output of our trained generative neural networks without any post-processing.

**Code and models will be released soon. Please stay tuned.**


FAQ
---

* Can other types of GANs work in current setting?

The proposed contextual attention module is independent of GAN losses. We experimented with other types of GANs in Section 5.1 and WGAN-GP is used by default. Intuitively, during training, pixel-wise reconstruction loss directly regresses holes to the current ground truth image, while WGANs implicitly learn to match potentially correct images and supervise the generator with adversarial gradients. Both WGANs and reconstruction loss measure image distance with pixel-wise L1.

* How to determine if G is converged?

We use a slightly modified WGAN-GP for adversarial loss. WGANs are demonstrated to have more meaningful convergent curves than others, which is also confirmed in our experiments.

* The split of train/test data in experiments.

We use the default training/validation data split from Places2 and CelebA. For CelebA, training/validation have no identity overlap. For DTD texture dataset which has no default split, we sample 30 images for validation.

* How does random mask generated?

Please check out function `random_bbox` and `bbox2mask` in file [inpaint_ops.py](/inpaint_ops.py).

* Parameters to handle the memory overhead.

Please check out function `contextual_attention` in file [inpaint_ops.py](/inpaint_ops.py).
