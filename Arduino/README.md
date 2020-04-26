This folder contains the arduino project for the 4-axis CMM arm.

I saw several other, somewhat similar projects with Arduino code.  However, it was a little hard to understand exactly what they were doing, and I decided to write the code entirely on my own.

The strategy, which I have nt seen in any of the other projects is to use interrupt-based recording of the encoder positions.  I use pin change interrupts for all the encoders.  I try to split the encoders across all the available ports in order to reduce the interrupt processing for any single interrupt.

Certainly all the encoders could occupy a single port, and it may actually be faster overall to do so.  I have not compared overhead processing of the interrupt for 1, 2 and more encoders on a single port versus spread over multipe ports.

I believe the use of interrupts is superior to the use of a timer, which could miss encoder transistions if they occur too quickly, and also occupies a lot of CPU time polling the encoder pins even when they are not changing.

The software also allows for single point reading, as well as high speed continuoous point reading.  I believe the maximum bandwidth is maybe up to 70 readings/second, but this seems to be excessively fast.  The software uses a timer to pace the readings (not a timer to poll the encoders).  Between readings, the encoder counters may well get updated many times.
