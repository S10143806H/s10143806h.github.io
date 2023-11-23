# Gaussian Blur

## Objective
A lightweighted algorithm is needed to implement the image processing in a micro controller

![](http://blog.dzl.dk/wp-content/uploads/2019/06/blur1-768x954.jpg =300x400)

In case of 32-pixel wide sensor image:

![](http://blog.dzl.dk/wp-content/uploads/2019/06/subMap1-768x342.jpg)


## Code
```
// Gaussian Blur 
#include "GaussianBlur.h"
GBlur blur;
float SubPixel[3072];        // pixel 32*24 *4

// get Gaussian Blur Data 32*2 * 24*2 -> 64*48
blur.calculate(mlx90640To, SubPixel);

for (int i = 0; i < 3072; i++){
     if (_MAX_T < SubPixel[i]) _MAX_T = SubPixel[i];
     if (_MIN_T > SubPixel[i]) _MIN_T = SubPixel[i];
   }  
   
for (int i = 0; i < 3072; i++)  {
    c = GetColor(SubPixel[i]);
    // Draw image pixels (rectangles):
    tft.fillRect(x, y, 3, 3, c);

    x = x -3;
    if (i % 64 == 63)
    {
      x = start_x + 63 * 3 -3;
      y = y + 3;
    }
  }
  
float ReadRate = 1000.0 / (TimeFlag[1] - TimeFlag[0]);
float ExpandPixel = (TimeFlag[2] - TimeFlag[1]);
float ReadpusPrintRate = 1000.0 / (TimeFlag[3] - TimeFlag[0]);
  
```
## References

[1] Compact Gaussian interpolation for small displays 
http://blog.dzl.dk/2019/06/08/compact-gaussian-interpolation-for-small-displays/?fbclid=IwAR0xl4af_NuDFRM94nuo1NksOQXc_3omvz7sQQVZ0UqG_TxKMjU4KtDcpmo

[2] Gaussian Kernel Calculator
https://dev.theomader.com/gaussian-kernel-calculator/