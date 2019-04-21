---
title: '[Notes] Shapes of CNN'
date: 2019-04-21
permalink: /posts/2019/04/blog-post-3/
tags:
   - Convolutional neural network
---

Since the size of input after convolving, padding and max-pooling can be tricky, I believe having  formula sheet that keeps track of the shape after eaceh operation will come in handy. So, here we go.

Let the input X be a matrix of shape $$(n_h,n_w,n_c)$$ and F be a filter of shape $$(f_h,f_w,f_{cin},f_{cout})$$, then output of $$X\circledast F$$ will be of shape $$(n_h-f_h+1,n_w-f_w+1,f_{cout})$$. Here,
f_cout can be understood as the number of filters.

Now, consider padding $p$ and stride $s$. $$X\circledast F$$ will be of shape $$(n_h+2*p-f_h+1,n_w+2*p-f_w+1,f_{cout})$$.