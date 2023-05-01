Download Link: https://assignmentchef.com/product/solved-cad2122-project-1
<br>
Image filters, like the blur filter used in lab 3, are examples of matrix processing that can be taken to the GPU. Consider two classes of filters: area filters, that considers an area around each pixel to define the final value of that pixel; and the point filters, that applies some function on the pixel value. For this project you need to implement a sequence of two filters with some parameters, that could be applied to any given image.

For the area filter, considering just the direct neighbors, we get a 3×3 grid of pixels with the original pixel at its center.




The final value for that pixel will be the weighted average defined by a 3×3 matrix of coefficients. The following examples of coefficients allows the implementation of several types of filters:




For the point filter, we pretend to gray the image using the following expression:

(r,g,b) = alpha*(c,c,c) + (1-alpha)(r,g,b),  where c = 0.3 r + 0.59 g + 0.11 b Alfa is a value in [0 .. 1] that defines the color shift to grayscale.




A sequential code example is provided for reference. The main objective is to achieve the best performance, particularly for big images. For convenience, this work is presented in several stages (number 5 is mandatory):




<ol>

 <li>(30%) Implement a CUDA or OpenCL solution that

  <ol>

   <li>Parallelizes both filter operations</li>

  </ol></li>

</ol>

Suggestion: experiment with different parallel strategies. Examples: just one kernel with both filters vs. one kernel per filter.

<ol>

 <li>Experiment with different grid layouts and block sizes.</li>

</ol>

Study if using a local shared area can improve your kernel(s) performance (nvprof and section 8 of CUDA Best Practices Guide<a href="#_ftn1" name="_ftnref1"><sup>[1]</sup></a> may help you evaluate any improvement).




<ol start="2">

 <li>(20%) Evaluate these solutions against

  <ol>

   <li>The sequential version</li>

   <li>Using different grid arrangements and thread block sizes</li>

   <li>Using/not using shared memory</li>

  </ol></li>

</ol>

Note: ignore file I/O times but include in your timings memcopy to/from device.

<strong>                </strong>







<ol start="3">

 <li>(15%) Complement your solution with the ability to overlap computation with communication by partitioning the image space to process into a given number of partitions (NP). Assigning each of such partitions to a dedicated stream. Consider the following example with NP=3.</li>

</ol>







While kernel(s) is(are) being applied over Partition 2, Partition 3 can be simultaneously uploaded to the GPU and, possibly, the result of processing Partition 1 can be simultaneously downloaded from the GPU.




<ol start="4">

 <li>(15%) Evaluate this solution against the others.</li>

</ol>




<ol start="5">

 <li>(20%) Write a report (max of 5 pages A4 11pt font) that presents

  <ol>

   <li>Tested approaches and final solution</li>

   <li>Relevant implementation details</li>

   <li>Your evaluation results (include times and/or graphs to compare and justify your solution)</li>

   <li>An analysis and interpretation of these results</li>

  </ol></li>

</ol>




Other relevant optimizations may also be accounted in the final grade.

<a href="#_ftnref1" name="_ftn1">[1]</a> https://docs.nvidia.com/cuda/cuda-c-best-practices-guide/index.html#performance-metrics