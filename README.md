# CMM-Arm

<a href="https://github.com/Tek-User/CMM-Arm/blob/master/Photos/Extended-1.jpg"><img src="https://github.com/Tek-User/CMM-Arm/blob/master/Photos/Extended-1.jpg" width="500px"><br/></a>

Development of an accurate, inexpensive DIY CMM arm

This project uses, as much as possible, 3D printed parts.  However, the rigidity of plastic arm sections is sub-optimal, and hollow section aluminum arm segments with 3D printed connectors may be required for good accuracy.  Right now I have about +/-1mm accuracy if I am careful when I take the measurements and avoid twisting any arm segments, and keep the arm angles away from the extremes.

This has the potential to be a really good machine to obtain reasonably accurate X-Y-Z measurements.  However, real-world issues impede this goal.  If we can solve the following issues, then we have a great device!  I am looking for any input to solve these issues.

Issues: RIGID PARTS

I have printed larger cross section arm segments.  These are, indeed, much more rigid.  But I found that the resulting arm segment has a curvature.  Oddly, it is concave TOWARD the printer bed.  I am not sure WHY this is occurring, so I have not found a solution.  Narrower cross section parts appear to have little or no curvature.

This project is definitely "In Progess", but it is functional now.  It has about +/-1mm reproducibility with the arm segments in different positions, and with the pointer tip in the same XYZ location.

Issues: CALIBRATION

Regarding accuracy: to have good accuracy, you need a good calibration!  There are 3 factors that have an influence.  The calculation of the XYZ position is based on the length and position of each of 5 parts: the base, the shoulder, and each of the 3 arm segments.  This assumes there is no wobble of the axes in the encoder mechanism, and there is no bending/twisting of the arm segments!

1)  While we know the nominal lengths of the parts based on the CAD design, we do not know the actual length to 2 or 3 decimal places.  And the length is likely temperature sensitive, so if the temperature is different from the time that the exact length was determined, then the length estimates are likely wrong.

2)  We need to zero the position of the encoders.  The encoders measure relative rotation, so we need to know where they started.  I use a very crude method to zero the "elbow", and "wrist" encoders.  The "pivot" and shoulder encoders's starting positions are not critical to get good measurements of one XYZ position compared to another.  The relative positions are unaffected.  But if we need absolute position compared to the rest of the world, then we need an accurate zero of the pivot and shoulder encoders.

3)  We do not know the exact angle of joints.  I use encoders with as high a resolution as possible.  They are rated as "2000 p/r".  Quadrature encoders will have 4x as many quadrature transitions than that, so my encoders have an angular resolution of 1/8000 of a full circle.  With the arm fully extended it has a length of 200+150+100 = 450mm.  The pivot has a resolution of 1/8000 of the full circle (7.85e-4 radians). That means that the XYZ position resolution of the tip of the arm when fully extended is about 450 * 7.84e-4 (rule of thumb that the sine of a small angle equals the angle in radians).  This equals about 0.35mm.  And the inaccuracy propagates down the chain of arm sections and encoders, each amplifying the error of the previous ones.

So, we need to be able to zero the system regarding the exact length of each part of the system, and the exact angular position of them.  I THINK that a bunch of measurements of a standard item could be be used in simultaneous equations to solve for lengths and rotations of each part.  However, when I tried to grapple with that problem, my brain instantly started to fry.  I hope that someone out there can solve this conundrum.  I believe that a maybe an 8x8 matrix can be used to solve for starting points (zero positions and lengths).  But it is beyond me to solve it, or even verify that the general mathematical solution is correct!


AN ITEM LEFT TO DO:
Write a PC program (portable to other platforms) to record the ascii XYZ readings coming from the Arduino and save it to a file on the PC.  In addition it should show the point cloud in real-time as the data is being generated so we can be sure tht we have mapped all the required surface of the object.  Java or Python might be reasonable programming languages for an open source programming environment.  I have some experience with Java, and no experience with Python.


POST PROCESSING:
Right now I use an assemblage of freeware to take the point cloud and generate a mesh.  I use Meshlab for this.  But I find this cumbersome to work with in general, so I aso use MeshMixer and Blender to re-scuplt the mesh.  Once we get improved accuracy of the XYZ readings, then there will be much reduced need to massage the mesh!!!
