# Coloured shapes detection
This project is implemented using **OpenCV** to detect basic geometric shapes in an image and determine their corresponding colours.

## How does it work?
- **Image loading & Preprocessing:**
  - The input image is read using ```cv2.imread``` then resized to a fixed resolution to ensure accurate detection.
  - Then, the resized image is converted to **grayscale**.
  - After that, **Binary inverse thresholding** is applied to separate shapes from the background.
  - Finally, external contours are extracted using ```cv2.findContours```.


- **Shape Detection:**
  - Each detected contour is approximated using ```cv2.approxPolyDP```.
  - The number of vertices in the approximated contour is used to classify shapes:
    Triangle --> 3 vertices<br />
    Square --> 4 vertices, *verified using an aspect ratio check (width/height with tolerance) to avoid confusion with lines.*<br />
    Circle --> approximated contours with 6–8 vertices<br />
    Line --> contours that do not match the above conditions<br />
  - Finally, bounding rectangles are used to compute the aspect ratio and to position labels on detected shapes

- **Colour Detection:**
  - First, the processed image is converted to the **HSV colour space**
  - Then, a binary mask is created for each contour.
  - The **mean hue value** inside the contour mask is calculated
  - At the end, colours are classified based on predefined hue ranges:
    *Red<br />
    Yellow<br />
    Green<br />
    Blue*<br />
  If the hue does not fall within these ranges, the shape is labelled as "Colour cannot be detected

- **Annotation & Output:**
Contours are drawn on the image and each detected shape is labelled with its **geometric type** and its **detected colour**. Finally, they are all saved to an output directory.

- **Dependencies:**
   - Python
   - OpenCV
   - NumPy
