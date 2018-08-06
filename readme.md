# MPTT Charge Controller

Reference Design: http://www.ti.com/tool/TIDA-00120

## Resources

- How Buck Converters work (video is super helpful): https://electronicsforu.com/videos-slideshows/diy-buck-converter-tutorial
- DIY MPTT Charge Controller: http://coder-tronics.com/c2000-solar-mppt-tutorial-pt1/. This explains how to build a buck converter that is very efficient (see notes below).

## Theory of Operation

### Buck Converter

The basics of a buck converter are simple and are well-explained in the above link. Use PWM and a MOSFET to reduce the average voltage. Add an inductor to smooth the current. Add a diode to create a current path when the MOSFET is off. Add a capacitor to smooth the voltage. Finally, some voltage feedback mechanism is necessary to adapt the PWM duty cycle to keep the voltage constant.

#### Efficiency (see resources for overview)

There a few efficiency problems with the basic buck converter design:

1. The voltage drop of the diode.
2. Output ripple.
3. Switching losses in the MOSFET.

(1) is addressed by replacing the diode with a MOSFET and toggling it opposite the main MOSFET. The main MOSFET is known as the high-side and the other is the low-side. I believe this is called a half-bridge but I'm not certain.
(2) is addressed by what's known as an *interleaved* design. This places two circuits in parallel, which supposedly halves the ripple. _TODO: understand why_.
(3) is minimized by a few factors:
1. Low RDS(on) MOSFET.
2. Low Rise/Fall time MOSFET.
3. Selection of switch frequency. A higher frequency will reduce output ripple but increase switching losses, and vise-versa.


