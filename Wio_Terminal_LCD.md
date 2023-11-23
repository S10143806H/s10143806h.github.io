# Wio Terminal LCD

## Pixel Coordinates Systems
A digital 2-D image is made up of rows and columns of pixels. A pixel in the image is specified by saying which column and which row the pixel is in. In simple terms, a pixel can be identified by a pair of integers providing the column number and the row number. For example, the pixel with coordinates (4,7) would lie in column 4, and row 7.
![](https://files.seeedstudio.com/wiki/Wio-Terminal/img/grids.jpg)


## Print MLX Result to LCD

![](https://i.imgur.com/95sJNFL.png)

## Code

```
   for (int i = 0; i < 768; i++)  {
     // Display a simple image version of the collected data (array) on the screen:
     // Define the color palette:
     c = GetColor(mlx90640To[i]);
     // Draw image pixels (rectangles):
     tft.fillRect(x, y, 6, 6, c);

     x = x - 6;
     if (i % 32 == 31) {
       x = start_x + 31 * 6 ;
       y = y + h;
     }
   }

```