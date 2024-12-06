# CS663_Final_Project
### JPEG Image Compression Engine for grayscale images. RMSE vs BPP results on 9 images have been performed.

---

I used two different functions to write the encoded image into file. One was used for the decoding part and the other was used to evaluate BPP. The reason for doing this is that in the former, the metadata was too large and it skewed the RMSE vs BPP results. In the latter, the encoded bitstream only includes the information that is absolutely necessary to decode the image, reducing the metadata and giving correct BPP results. With the latter function I was able to get results that closely matched OpenCV's compression algorithm although it wasn't as good since mine is a more naive implementation.
