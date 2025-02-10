# Image Segmentation using HSV Color Space

This program implements image segmentation based on hue thresholds in the HSV color space. It takes an RGB image as input and produces an output where pixels within the specified hue range are displayed in their original color, while pixels outside this range are converted to grayscale.

## Screenshots
![Segmented Image 1](https://imgur.com/Bv9nHQt.png)
![Segmented Image 2](https://imgur.com/Jt4iV1R.png)


## Usage

The program takes three command-line arguments:

```bash
image.exe <input_image_path> <h1> <h2>
```

- `<input_image_path>`: Path to the input RGB image file (512x512 pixels, 24-bit color)
- `<h1>`: First hue threshold (0-360)
- `<h2>`: Second hue threshold (0-360), must be greater than h1

## Implementation Details

1. The program reads the input RGB image (512x512 pixels, 24-bit color).
2. It converts the RGB values to HSV color space for each pixel.
3. For each pixel, it checks if the hue value falls within the range [h1, h2]:
   - If yes, the pixel retains its original color in the output.
   - If no, the pixel is converted to grayscale in the output.
4. The resulting segmented image is displayed.

## RGB to HSV Conversion

The RGB to HSV conversion is implemented using the following algorithm:

1. Normalize RGB values to the range [0, 1].
2. Calculate Chroma (C), Value (V), and Saturation (S).
3. Calculate Hue (H) based on which RGB component is max.
4. Adjust Hue to be in the range [0, 360].

## Grayscale Conversion

For pixels outside the specified hue range, grayscale conversion is done using the luminance formula:

```
Gray = 0.299 * R + 0.587 * G + 0.114 * B
```

## Example Outputs

1. `image.exe roses_image1.rgb 0 359`
   - Output: Same as input (all colors preserved)

2. `image.exe roses_image1.rgb 320 359`
   - Output: Red parts of the image preserved, rest in grayscale

3. `image.exe roses_image1.rgb 60 120`
   - Output: Green parts of the image preserved, rest in grayscale

## Notes

- Ensure the input image is in the correct format (512x512 pixels, 24-bit RGB).
- The program assumes h2 > h1. If h2 < h1, the behavior is undefined.
- For best results, use images with distinct color regions.
