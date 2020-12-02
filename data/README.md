# Binary Star System Data
This is a dataset for a fictional universe - a binary star system. There are two "suns", one "Earth" and one "moon" in this system. Two "suns" are orbiting each other in a cirlce, with a diameter of 0.2 AU. The mass of each fictional "sun" is half of the real sun mass. The fictional "Earth" ("moon") orbit is set to be close to the real Earth (moon) orbit as much as possible. All orbits are in the same plane. The time zero is when four planets are collinear, while the "Earth" is at perihelion and the "moon" is at apogee.

## Data Format
Our data consists of two parts:

1. Simulation data: generated using Mathematica n-body simulation and coordinates transformation.
2. SpaceEngine data: generated using OCR on SpaceEngine screenshots 

### Simulation data
Trajectories simulation are generated using Mathematica 4-body simulation. The positions of all four planets are presented in a cartesian coordinate system, whose origin coincides with the mass center of the two suns. All dynamics are within xy-plane. We also include z-axis data, which should be all zero, in case people want to include z-axis motion in future. The code is stored in ```simulation_data/binary_star_simulation.nb ```, while the data are stored in ```simulation_data/coordinates_evolution.csv ```. Time is in the units of seconds, while coordinates are in the units of meters. The data file has the following formats:

|Time|SunA_x|SunA_y|SunA_z|SunB_x|SunB_y|SunB_z|earth_x|earth_y|earth_z|moon_x|moon_y|moon_z|
|---|---|---|---|---|---|---|---|---|---|---|---|---|
|...|...|...|...|...|...|...|...|...|...|...|...|...|

Apart from that, we also generated observation data under observer's topocentric coordinate system, which includes azimuth and altitude, by applying correct coordinate transformation to trajectories. We have three such files in three different observer locations: Berkeley (```simulation_data/berkeley_azi_alt.csv ```), Shanghai (```simulation_data/shanghai_azi_alt.csv ```) and Sydney (```simulation_data/sydney_azi_alt.csv ```). Each of them has the following format (time in units of seconds, others in degrees):

|Time|SunA_azimuth|SunA_altitude|SunB_azimuth|SunB_altitude|moon_azimuth|moon_altitude|
|---|---|---|---|---|---|---|
|...|...|...|...|...|...|...|

The code used to transform trajectories to the observations is stored in ```simulation_data/coordinates_to_azimuth_altitude.ipynb```. In theory, one can change the longitude and the latitude to an arbitray located observer, and generate data under such observation coordinate system.


### SpaceEngine data
We first input the approximated trajectories into SpaceEngine. Then we chose the three above mentioned positions (Berkeley, Shanghai and Sydney) to generate screenshots which include measurables. All screenshots are stored here: [Raw Data](https://drive.google.com/drive/folders/1Ee4sjJTGXAE0LJyyK6H0fr3iWYFP0aoU?usp=sharing). Finaly we used trained Optical Character Reader (OCR) to recognize numbers and output them in csv files. We include an example OCR data generation using [Mathpix](https://docs.mathpix.com/#introduction). The generated csv files are stored in ```observations/generated_data```. One can regenerate the csv files once screenshots load path and Mathpix key are configured in the Jupyter notebook.

There are three folders named *Berkeley*, *Shanghai* and *Sydney* in generated data. Each folder contains the following information. 

#### *_location.csv
The location file stores the observer's latitude and longtitude information on Earth. Below is the format:

|latitude_degree|latitude_minute|latitude_second|longtitude_degree|longtitude_minute|longtitude_second|
|---|---|---|---|---|---|
|...|...|...|...|...|...|

#### *_sun_a.csv & *_sun_b.csv
These two types of files contain the observation information of the two stars SunA and SunB in our binary star solar system.
Each file has the following format:
Figure index, Time, Direction(azimuthal angle), Height(polar angle), Apparent size

1. Figure index indicates the corresponding figure for generating this line of data.
2. Time is the absolute time in our fictional universe(No time zone difference).
3. Direction is the azimuthal angle of the Sun observed from the given location in spherical coordinates.
4. Height is the polar angle of the Sun observed from the given location in spherical coordinates.

For Time, the format in the file is: year month day hour minute second   
For Direction, Height, and Apparent size, the format in the file is: degree minute second. The complete format table is as below:

|index|year|month|day|hour|minute|second|azi_deg|azi_min|azi_sec|pol_deg|pol_min|pol_sec|size_deg|size_min|size_sec|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|...|...|...|...|...|...|...|...|...|...|...|...|...|...|...|...|

#### *_moon.csv
The format is the same as that of *_sun_a.csv and *_sun_b.csv except for an additional data column recording the phase of moon. The phase of moon should be a number between 0 and 1. The complete format table is as below:

|index|year|month|day|hour|minute|second|azi_deg|azi_min|azi_sec|pol_deg|pol_min|pol_sec|size_deg|size_min|size_sec|phase|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|...|...|...|...|...|...|...|...|...|...|...|...|...|...|...|...|...|

## Authors
* Zheyu Lu   
* Rui Liu   
* Shuqi Xu


