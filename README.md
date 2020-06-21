# SFND_Radar_Target_Generation_and_Detetion

1. **FMCW Waveform Design**<br>
Using the given system requirements, design
a FMCW waveform. Find its Bandwidth (B), chirp time (Tchirp) and slope of the chirp. For given system requirements the calculated slope should be around 2e13.<br>

2. **Simulation Loop**<br>
Simulate Target movement and calculate the beat or mixed signal for every timestamp. A beat signal should be generated such that once range FFT implemented, it gives the correct range i.e the initial position of target assigned with an error margin of +/- 10 meters.<br>

3. **Range FFT (1st FFT)**<br>
Implement the Range FFT on the Beat or Mixed Signal and plot the result. A correct implementation should generate a peak at the correct range, i.e the initial position of target assigned with an error margin of +/- 10 meters.<br>

4. **2D CFAR**<br>
Implement the 2D CFAR process on the output of 2D FFT operation, i.e the Range Doppler Map. The 2D CFAR processing should be able to suppress the noise and separate the target signal. The output should match the image shared in walkthrough.<br>



## CFAR Implementation:
* Determine the number of Training cells for each dimension. Similarly, pick the number of guard cells.
* Slide the cell under test across the complete matrix. Make sure the CUT has margin for Training and Guard cells from the edges.
* For every iteration sum the signal level within all the training cells. To sum convert the value from logarithmic to linear using db2pow function.
* Average the summed values for all of the training cells used. After averaging convert it back to logarithmic using pow2db.
* Further add the offset to it to determine the threshold.
* Next, compare the signal under CUT against this threshold.
* If the CUT level > threshold assign it a value of 1, else equate it to 0.


## Selection of Training, Guard cells and offset
* Number of Training cells in range dimension (TR) = 10
* Number of Training cells in doppler dimension (TD) = 8
* Number of Guard cells in range dimension (GR) = 4
* Number of Guard cells in doppler dimension (GD) = 4
* Offset = 1.4 <br>

**Note**: Observe the distribution of the signal, to select the size of the guard cells.
<br>

## Suppressing non-Threshold cells:
* RDM(union(1:(TR+GR),end-(TR+GR-1):end),:) = 0;  // Rows
* RDM(:,union(1:(TD+GD),end-(TD+GD-1):end)) = 0; // Columns  

where,<br>
TR -> no. of training cells in range dimension<br>
TD -> no. of training cells in doppler dimension<br>
GR -> no. of guard cells in range dimension<br>
GD -> no. of guard cells in doppler dimension<br>
RDM -> Range Doppler Map<br>
