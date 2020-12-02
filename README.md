# Project-S-final
We create a fictional binary star solar system which has two suns, one Earth and one moon. In our
early project, we generate our data by using SpaceEngine and OCR. This time, however, we come up
with a new method to generate the altitude and azimuth data of the celestial bodies by analytically
solving our model which generalized and simplified our previous method. Our current method can
be used to quickly generate observation data from an arbitrary position on Earth. Combining the
two methods can provide us with abundant data for learning the orbital motion and positions of the
celestial bodies and the moon phase.<br>
Our results can be used to further study and predict both solar and lunar eclipse phenomena since we
can accurately predict the time evolution curve of the sun’s and the moon’s position on the sky. That
will be an interesting work for us in the future.<br>
The paper is organized as follows: In Section 2, we firstly introduce data generation in Section
2.1 which includes the two different methods we used to generate our data and we also verify the
consistency between using the two methods. For the second method, we also introduce the theory
and show the analytical derivation of the coordinate transformation. In Section 2.2, we discuss the
physical intuition when we analyzed the data and chose the relevant features. This can be viewed as
preprocessing the data with reasonable physical consideration and certain domain knowledge. The
main learning results of the position of the celestial bodies and the moon phase are shown in Section
3. In Section 4, we conclude the results we learned and also discuss the underlying physics which is
related to the observed astronomical phenomena.
