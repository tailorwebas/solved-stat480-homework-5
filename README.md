Download Link: https://assignmentchef.com/product/solved-stat480-homework-5
<br>



<h1>0.   Data Preparation (Command line commands)</h1>

<em># Download dataset </em>

cd ~/Stat480/hb-workspace/input/ncdc chmod u+x ncdc_data.sh ./ncdc_data.sh 1915 1924 <em># Copy data to Hadoop </em>

hadoop fs -put ~/Stat480/hb-workspace/input/ncdc/all/* input/ncdc/HW5

<em># Go to python files stored folder </em>

cd ~/Stat480/hb-workspace/ch02-mr-intro/src/main/python




<h1>1.   Exercise 1</h1>

Using Hadoop and MapReduce, find the minimum monthly recorded air temperature from 1915 to 1924 and return those minimum values in degrees Celsius. (You should have 12 values total, one for each month).




<strong>Map script:</strong> min_temperature_map.py <strong>Reduce script:</strong> min_temperature_reduce.py <strong>Command line commands: </strong>

<em>            # Create new map/reduce file by copying and editing the exists </em>cp max_temperature_map.py min_temperature_map.py cp max_temperature_reduce.py min_temperature_reduce.py




<em># Open and edit python map/reduce files </em>

vi min_temperature_map.py vi min_temperature_reduce.py




<em>            # Run MapReduce </em>

hadoop jar /usr/lib/hadoop-mapreduce/hadoop-streaming.jar 

-files /home/binfeng2/Stat480/hb-workspace/ch02-mr-intro/src/main/python/ min_temperature_map.py, /home/binfeng2/Stat480/hb-workspace/ch02-mrintro/src/main/python/min_temperature_reduce.py 

-input input/ncdc/HW5/ 

-output outputpy 

-mapper “/home/binfeng2/Stat480/hb-workspace/ch02-mr-intro/src/main/python/ min_temperature_map.py” 

-reducer “/home/binfeng2/Stat480/hb-workspace/ch02-mr-intro/src/main/python/ min_temperature_reduce.py”




<em># Show results </em>

hadoop fs -cat outputpy/part*




<em># Delete directory </em>hadoop fs -rm -r -f outputpy




<strong>Results: </strong>

<table width="426">

 <tbody>

  <tr>

   <td width="150"><strong>Month </strong></td>

   <td width="276"><strong>Min Temperature (Celsius) </strong></td>

  </tr>

  <tr>

   <td width="150">01</td>

   <td width="276">-45.6</td>

  </tr>

  <tr>

   <td width="150">02</td>

   <td width="276">-47.8</td>

  </tr>

  <tr>

   <td width="150">03</td>

   <td width="276">-39.4</td>

  </tr>

  <tr>

   <td width="150">04</td>

   <td width="276">-31.1</td>

  </tr>

  <tr>

   <td width="150">05</td>

   <td width="276">-7.8</td>

  </tr>

  <tr>

   <td width="150">06</td>

   <td width="276">-2.8</td>

  </tr>

  <tr>

   <td width="150">07</td>

   <td width="276">1.1</td>

  </tr>

  <tr>

   <td width="150">08</td>

   <td width="276">0.0</td>

  </tr>

  <tr>

   <td width="150">09</td>

   <td width="276">-13.9</td>

  </tr>

  <tr>

   <td width="150">10</td>

   <td width="276">-28.9</td>

  </tr>

  <tr>

   <td width="150">11</td>

   <td width="276">-36.1</td>

  </tr>

  <tr>

   <td width="150">12</td>

   <td width="276">-42.8</td>

  </tr>

 </tbody>

</table>




The table above shows results queried for the minimum monthly recorded air temperature in degrees Celsius from 1915 and 1924. Note that all months’ minimum temperatures are below or equal 0 degree Celsius except July. The minimum temperature among all months is -47.8 degree Celsius recorded in February.




<h1>2.   Exercise 2</h1>

Using Hadoop and MapReduce, obtain the number of trusted temperature observations and the minimum and maximum monthly temperatures in degrees Fahrenheit over the period of 1915 to 1924. Make sure your code only goes through the data once to get these results (to do this you will need to update the minimum, maximum, and count at the same step in the code).




<strong>Map script:</strong> trust_max_min_temperature_map.py <strong>Reduce script:</strong> trust_max_min_temperature_reduce.py <strong>Command line commands: </strong>

<em>            # Create new map/reduce file by copying and editing the exists </em>cp max_temperature_map.py trust_max_min_temperature_map.py cp max_temperature_reduce.py trust_max_min_temperature_reduce.py

<em> </em>

<em># Open and edit python map/reduce files </em>vi trust_max_min_temperature_map.py vi trust_max_min_temperature_reduce.py

<em> </em>

<em># Run MapReduce</em>

hadoop jar /usr/lib/hadoop-mapreduce/hadoop-streaming.jar 

-files /home/binfeng2/Stat480/hb-workspace/ch02-mr-intro/src/main/python/ trust_max_min_temperature_map.py, /home/binfeng2/Stat480/hb-workspace/ch02-mr-intro/src/main/python/ trust_max_min_temperature_reduce.py 

-input input/ncdc/HW5/ 

-output outputpy 

-mapper “/home/binfeng2/Stat480/hb-workspace/ch02-mr-intro/src/main/python/ trust_max_min_temperature_map.py” 

-reducer “/home/binfeng2/Stat480/hb-workspace/ch02-mr-intro/src/main/python/t rust_max_min_temperature_reduce.py”




<em># Show results </em>

hadoop fs -cat outputpy/part*




<em># Delete directory </em>

hadoop fs -rm -r -f outputpy




<strong>Results: </strong>

<table width="582">

 <tbody>

  <tr>

   <td width="68"><strong>Month </strong></td>

   <td width="198"><strong>Max Temperature (Fahrenheit) </strong></td>

   <td width="158"><strong>Min Temperature (Fahrenheit) </strong></td>

   <td width="158"><strong>Observations </strong></td>

  </tr>

  <tr>

   <td width="68">01</td>

   <td width="198">44.96</td>

   <td width="158">-50.08</td>

   <td width="158">6500</td>

  </tr>

  <tr>

   <td width="68">02</td>

   <td width="198">44.96</td>

   <td width="158">-54.04</td>

   <td width="158">6003</td>

  </tr>

  <tr>

   <td width="68">03</td>

   <td width="198">62.96</td>

   <td width="158">-38.92</td>

   <td width="158">6572</td>

  </tr>

  <tr>

   <td width="68">04</td>

   <td width="198">77.0</td>

   <td width="158">-23.98</td>

   <td width="158">6285</td>

  </tr>

  <tr>

   <td width="68">05</td>

   <td width="198">82.94</td>

   <td width="158">17.96</td>

   <td width="158">6571</td>

  </tr>

  <tr>

   <td width="68">06</td>

   <td width="198">89.06</td>

   <td width="158">26.96</td>

   <td width="158">6342</td>

  </tr>

  <tr>

   <td width="68">07</td>

   <td width="198">100.04</td>

   <td width="158">33.98</td>

   <td width="158">6581</td>

  </tr>

  <tr>

   <td width="68">08</td>

   <td width="198">86.0</td>

   <td width="158">32.0</td>

   <td width="158">6505</td>

  </tr>

  <tr>

   <td width="68">09</td>

   <td width="198">75.92</td>

   <td width="158">6.98</td>

   <td width="158">6183</td>

  </tr>

  <tr>

   <td width="68">10</td>

   <td width="198">62.06</td>

   <td width="158">-20.02</td>

   <td width="158">6502</td>

  </tr>

  <tr>

   <td width="68">11</td>

   <td width="198">50.0</td>

   <td width="158">-32.98</td>

   <td width="158">6294</td>

  </tr>

  <tr>

   <td width="68">12</td>

   <td width="198">50.0</td>

   <td width="158">-45.04</td>

   <td width="158">6504</td>

  </tr>

 </tbody>

</table>




The table above shows results queried for the number of trusted temperature observations and the minimum and maximum monthly temperatures in degrees Fahrenheit over the period of 1915 to 1924. Note that all months’ maximum temperatures are above 0 degree Fahrenheit with the maximum of all at 100.04 degree Fahrenheit in July. And month 1, 2, 3, 4, 10, 11, and 12 have minimum temperatures below 0 degree Fahrenheit. The minimum temperature among all months is -54.04 degree Fahrenheit recorded in February. The number of observations are quite equal among all months.




<h1>3.   Exercise 3</h1>

Using Hadoop and MapReduce, obtain the total number of air temperature observations that are not missing for each month during the period from 1915 to 1924 and the total number of observations with acceptable quality codes for each month during that period. Make sure your code only goes through the data once to get these results (to do this, you could have the mapper return (month, tempcount, validqcount) for each observation, and have the reducer aggregate).

<strong>Map script:</strong> count_temperature_map.py <strong>Reduce script:</strong> count_temperature_reduce.py <strong>Command line commands: </strong>

<em>            # Create new map/reduce file by copying and editing the exists </em>cp max_temperature_map.py count_temperature_map.py cp max_temperature_reduce.py count_temperature_reduce.py




<em># Open and edit python map/reduce files </em>vi count_temperature_map.py vi count_temperature_reduce.py




<em># Run MapReduce</em>

hadoop jar /usr/lib/hadoop-mapreduce/hadoop-streaming.jar 

-files /home/binfeng2/Stat480/hb-workspace/ch02-mr-intro/src/main/python/ count_temperature_map.py,

/home/binfeng2/Stat480/hb-workspace/ch02-mr-intro/src/main/python/ count_temperature_reduce.py 

-input input/ncdc/HW5/ 

-output outputpy 

-mapper “/home/binfeng2/Stat480/hb-workspace/ch02-mr-intro/src/main/python/ count_temperature_map.py” 

-reducer “/home/binfeng2/Stat480/hb-workspace/ch02-mr-intro/src/main/python/ count_temperature_reduce.py”




<em># Show results </em>

hadoop fs -cat outputpy/part*




<em># Delete directory </em>hadoop fs -rm -r -f outputpy




<strong>Results: </strong>

<table width="424">

 <tbody>

  <tr>

   <td width="68"><strong>Month </strong></td>

   <td width="198"><strong>Air Temperature Observations </strong></td>

   <td width="158"><strong>Quality Code </strong><strong>Observations </strong></td>

  </tr>

  <tr>

   <td width="68">01</td>

   <td width="198">6500</td>

   <td width="158">6500</td>

  </tr>

  <tr>

   <td width="68">02</td>

   <td width="198">6003</td>

   <td width="158">6005</td>

  </tr>

  <tr>

   <td width="68">03</td>

   <td width="198">6572</td>

   <td width="158">6595</td>

  </tr>

  <tr>

   <td width="68">04</td>

   <td width="198">6285</td>

   <td width="158">6286</td>

  </tr>

  <tr>

   <td width="68">05</td>

   <td width="198">6571</td>

   <td width="158">6578</td>

  </tr>

  <tr>

   <td width="68">06</td>

   <td width="198">6342</td>

   <td width="158">6365</td>

  </tr>

  <tr>

   <td width="68">07</td>

   <td width="198">6581</td>

   <td width="158">6595</td>

  </tr>

  <tr>

   <td width="68">08</td>

   <td width="198">6505</td>

   <td width="158">6508</td>

  </tr>

  <tr>

   <td width="68">09</td>

   <td width="198">6183</td>

   <td width="158">6202</td>

  </tr>

  <tr>

   <td width="68">10</td>

   <td width="198">6502</td>

   <td width="158">6502</td>

  </tr>

  <tr>

   <td width="68">11</td>

   <td width="198">6294</td>

   <td width="158">6294</td>

  </tr>

  <tr>

   <td width="68">12</td>

   <td width="198">6504</td>

   <td width="158">6504</td>

  </tr>

 </tbody>

</table>




The table above shows results queried for the total number of air temperature observations that are not missing for each month during the period from 1915 to 1924 and the total number of observations with acceptable quality codes for each month during that period. Note that these two set of numbers quite similar with only a few differences. Also note that the number of observations are quite equal among all months.




<h1>4.   Exercise 4</h1>

Using Hadoop and MapReduce, obtain the monthly mean air temperature in degrees Celsius for the period from 1915 to 1924. If you use a combiner, make sure your code will work when data needs to be recombined from samples of different sizes.

<strong> </strong>

<strong>Map script:</strong> mean_temperature_map.py <strong>Reduce script:</strong> mean_temperature_reduce.py <strong>Command line commands: </strong>

<em>            # Create new map/reduce file by copying and editing the exists </em>cp min_temperature_map.py mean_temperature_map.py cp min_temperature_reduce.py mean_temperature_reduce.py




<em># Open and edit python map/reduce files </em>vi mean_temperature_map.py

vi mena_temperature_reduce.py




<em># Run MapReduce</em>

hadoop jar /usr/lib/hadoop-mapreduce/hadoop-streaming.jar 

-files /home/binfeng2/Stat480/hb-workspace/ch02-mr-intro/src/main/python/ mean_temperature_map.py,

/home/binfeng2/Stat480/hb-workspace/ch02-mr-intro/src/main/python/ mean_temperature_reduce.py 

-input input/ncdc/HW5/ 

-output outputpy 

-mapper “/home/binfeng2/Stat480/hb-workspace/ch02-mr-intro/src/main/python/ mean_temperature_map.py” 

-reducer “/home/binfeng2/Stat480/hb-workspace/ch02-mr-intro/src/main/python/ mean_temperature_reduce.py”




<em># Show results </em>

hadoop fs -cat outputpy/part*




<em># Delete directory </em>hadoop fs -rm -r -f outputpy <strong>Results: </strong>

<table width="346">

 <tbody>

  <tr>

   <td width="68"><strong>Month </strong></td>

   <td width="278"><strong>Mean Air Temperature (Celsius) </strong></td>

  </tr>

  <tr>

   <td width="68">01</td>

   <td width="278">-8.13858461538</td>

  </tr>

  <tr>

   <td width="68">02</td>

   <td width="278">-8.37404631018</td>

  </tr>

  <tr>

   <td width="68">03</td>

   <td width="278">-4.85763846622</td>

  </tr>

  <tr>

   <td width="68">04</td>

   <td width="278">1.01907716786</td>

  </tr>

  <tr>

   <td width="68">05</td>

   <td width="278">7.09373002587</td>

  </tr>

  <tr>

   <td width="68">06</td>

   <td width="278">12.0541784926</td>

  </tr>

  <tr>

   <td width="68">07</td>

   <td width="278">15.80205136</td>

  </tr>

  <tr>

   <td width="68">08</td>

   <td width="278">13.4259800154</td>

  </tr>

  <tr>

   <td width="68">09</td>

   <td width="278">9.11060973637</td>

  </tr>

  <tr>

   <td width="68">10</td>

   <td width="278">3.68974161796</td>

  </tr>

  <tr>

   <td width="68">11</td>

   <td width="278">-1.7658087067</td>

  </tr>

  <tr>

   <td width="68">12</td>

   <td width="278">-5.91194649446</td>

  </tr>

 </tbody>

</table>




The table above shows results queried for the monthly mean air temperature in degrees Celsius for the period from 1915 to 1924. Note that month 1, 2, 3, 11, 12 have mean air temperature below 0 with minimum mean temperature of all achieved in February for -8.37404631018 degree Celsius. The maximum mean temperature of all achieved in August for 13.4259800154 degree Celsius.


