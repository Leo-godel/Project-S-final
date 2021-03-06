# Fictional Universe: Binary Star System

## Introduction
We create a fictional binary star solar system which has two suns, one Earth and one moon. The initial condition of the system is shown below.

<p align="center">
  <img src="https://github.com/Leo-godel/Project-S-final/blob/media/init.png?raw=true", width="600px">
</p>

We generated data including all celestial bodies' coordinates in a cartesian coordinate system whose origin is the center-of-mass of the two suns, and azimuth, altitude, size of the two suns and the moon from an observer's point of view on Earth, as well as the lunar phase.

Based on the observation data from a local position on Earth, we use machine learning techniques and successfully learn the time evolution curve of the moon phase and the altitude and azimuth of the other three celestial bodies including the two suns and the moon.

## Data
In our early project, we generate our data by using SpaceEngine and OCR. This time, however, we come up with a new method to generate the altitude and azimuth data, of the celestial bodies by simulating their dynamics and analytically solving our model which generalized and simplified our previous method. Our current method can be used to quickly generate observation data from an arbitrary position on Earth. Combining the two methods can provide us with abundant data for learning the orbital motion and positions of the celestial bodies and the moon phase. In theory, the apparent size data can also be generated analytically based on this method. The analytically generated size, altitude and the azimuth data, together with SpaceEngine, can be used to further study and predict both solar and lunar eclipse phenomena. That will be an interesting work for us in the future.

The follwing part briefly explains two methods. Data and its format can be found [HERE](https://github.com/Leo-godel/Project-S-final/tree/main/data).

### SpaceEngine & OCR
We first input the approximated trajectories into SpaceEngine. Then we chose three locations on Earth-Berkeley, Shanghai and Sydney, to generate screenshots which include measurables. Finally we use OCR to recognize numbers and store them in csv files. 
### Simulation
We first generated trajectories of all celestial bodies' coordinates in a cartesian coordinate system whose origin is the center-of-mass of the two suns. Then we used rotation matrix to transform the coordinates to altitude and azimuth in observer's topocentric coordinate system. Mathematical details can be found [HERE](https://github.com/Leo-godel/Project-S-final/blob/main/writeup/Final_writeup.pdf).

## Training
### final_phase
From EDA and the observation of the data, we find the moon phase data is like a signle sinusoidal function:
<p align="center">
  <img src="https://github.com/Leo-godel/Project-S-final/blob/media/phase_formula.png?raw=true", width="100px">
</p>
Based on this assumption, we first guess the initial function. After that, we use a two-step way to fine-tune the parameters. First, we use gradient decent to fine-tune our parameters of the function. This step is intended to find the best w.
Since Asin(wx+c)+B is just a simple observation and the true function may contain other high order terms, just gradient decent is not enough.
After the gradient decent step, we construct a series of features like sin(wx) and cos(wx). Then, we do polynomial regression on them.

<strong>Result: </strong>
<p align="center">
  <img src="https://github.com/Leo-godel/Project-S-final/blob/media/result_pictures/moon_phase_test_plot.png?raw=true", width="800px">
</p>

### final_altitude
From EDA and the observation of the data, we find the altitude is like a combination of two sin function:
<p align="center">
  <img src="https://github.com/Leo-godel/Project-S-final/blob/media/altitude_formula.png?raw=true", width="280px">
</p>
Since learning the altitude and azimuth need a lot of data and gradient decent needs huge computation, our computers cannot finish enough iterations.
We use the function of fit in matlab to replace gradient decent in this part. 
After using matlab to get w1 and w2, we generate a series of features like sin(w1*t), cos(w1*t), sin(w2*t) and cos(w2*t). Then, as the previous part, we do polynomial regression.

<strong>Result: </strong>
<p align="center">
  <img src="https://github.com/Leo-godel/Project-S-final/blob/media/result_pictures/sunA_alt_test.png?raw=true", width="800px">
</p>
<p align="center">
  <img src="https://github.com/Leo-godel/Project-S-final/blob/media/result_pictures/sunA_alt_test_small.png?raw=true", width="800px">
</p>

### final_azimuth
Just from EDA and observation of the data, we cannot simply draw the function type of azimuth.
So, we try to use fourier features to fit the azimuth data.
First, we make the assumption that the basic frequency should be around 727, just like one frequency we find in altitude part.
Then, we fix the number of fourier features and use grid search method to fine-tune the basic frequency w.
Finally, we use the best w in previous step and gird search the best number of fourier features to get the final model.

<strong>Result: </strong>
<p align="center">
  <img src="https://github.com/Leo-godel/Project-S-final/blob/media/result_pictures/sunB_azi_test.png?raw=true", width="800px">
</p>

## Authors
* Zheyu Lu   
* Rui Liu   
* Shuqi Xu
