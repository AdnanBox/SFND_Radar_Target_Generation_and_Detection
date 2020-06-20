SFND_Radar_Target_Generation_and_Detetion


CFAR Implementation:
* Determine the number of Training cells for each dimension. Similarly, pick the number of guard cells.
* Slide the cell under test across the complete matrix. Make sure the CUT has margin for Training and Guard cells from the edges.
* For every iteration sum the signal level within all the training cells. To sum convert the value from logarithmic to linear using db2pow function.
* Average the summed values for all of the training cells used. After averaging convert it back to logarithmic using pow2db.
* Further add the offset to it to determine the threshold.
* Next, compare the signal under CUT against this threshold.
* If the CUT level > threshold assign it a value of 1, else equate it to 0.


Suppressing non-Threshold cells:
* RDM(union(1:(TR+GR),end-(TR+GR-1):end),:) = 0;  % Rows
* RDM(:,union(1:(TD+GD),end-(TD+GD-1):end)) = 0;  % Columns  

where,
TR -> no. of training cells in range dimension
TD -> no. of training cells in doppler dimension
GR -> no. of guard cells in range dimension
GD -> no. of guard cells in doppler dimension
RDM -> Range Doppler Map
