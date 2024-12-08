## The JPEG Algorithm
---

- **DCT**: The image is first padded, then DCT coefficients for each 8x8 block of the image are computed. The cosine basis here almost approximates the best basis, which was the eigenvectors of the covariance matrix in PCA. We usually subtract 128 from each value of the image before DCT computation so we can center the intensity values around 0.
- **Quantization**: We divide the DCT coefficient matrix element-wise by a quantization matrix that is already known and then round up the answers. We perform zigzag ordering on this matrix before RLE.
- **Run-Length Encoding**: This step gets rid of the redundancy while also completely storing each block to be used for Huffman encoding later. Tuples are of type (Run-length, Value).
- **Huffman Encoding**: This is a greedy algorithm, producing the least average bit length for a prefix-free encoding. For DC, we take their differences and run Huffman on that, while for AC, we directly run Huffman.
- **Writing to file**: I have added all of the important information including the dictionaries and bitstreams in the header for my files along with the quality factor.
- **Decoding**: The inverse of each of the above steps is computed, and the image is reconstructed and trimmed to meet the original shape.


With my implementation, I faced several bad aspects. Most importantly, the computation
time was significant. Also, the presence of block-seam artifacts as well as ringing artifacts.
Evidently, the algorithm does not work well on edges and corner features within an image.
Also, the fact that we have to store the bitstream, quantization matrix, and Huffman
dictionaries in the header for the files increases their size substantially. I assume that
machine learning methods for performing compression will be more efficient, especially if
parallel processing is applied to them.
