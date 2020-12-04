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
We first generated trajectories of all celestial bodies' coordinates in a cartesian coordinate system whose origin is the center-of-mass of the two suns. Then we used rotation matrix to transform the coordinates to altitude and azimuth in observer's topocentric coordinate system. Mathematical details can be found [HERE](https://github.com/Leo-godel/Project-S-final/blob/main/Final_writeup.pdf).

## Training
### final_phase
From EDA and the observation of the data, we find the moon phase data is like a signle sinusoidal function( Asin(wx+c)+B ). Based on this assumption, we first guess the initial function. After that, we use a two-step way to fine-tune the parameters. First, we use gradient decent to fine-tune our parameters of the function. This step is intended to find the best w.
Since Asin(wx+c)+B is just a simple observation and the true function may contain other high order terms, just gradient decent is not enough.
After the gradient decent step, we construct a series of features like sin(wx) and cos(wx). Then, we do polynomial regression on them.

### final_location
From EDA and the observation of the data, we find the altitude is like a composition of two sin function( A1sin(w1x+c1)+ A2sin(w2x+c2) + B )
Since learning the altitude and azimuth need a lot of data and gradient decent needs huge computation, our computers cannot finish enough iterations.
We use the function of fit in matlab to replace gradient decent in this part. 
After using matlab to get w1 and w2, we generate a series of features like sin(w1x), cos(w1x), sin(w2x) and cos(w2x). Then, as the previous part, we do polynomial regression.

## Authors
* Zheyu Lu   
* Rui Liu   
* Shuqi Xu
