# WORK IN PROGRESS

# Simple DC-DC converters

## 24 V to 5 V @ 1.5 A

This project will convert a regulated 24 VDC supply to 5 VDC using a switching regulator. Switch regulators
essentually reduce (buck), or boost a DC voltage to supply power to a device needing that specific voltage. 
A common design in a lot of projects requiring parts with different voltage supply levels is to first 
generate regulated power for supplying the part with the highest voltage requirement, and then converting 
that power down to the voltage levels needed by the other parts.

### BOM

As per regulator datasheet for 5V/500 mA design - we want more current, right!

* Switching Regulator: [MC33063A 1.5-A Peak Boost/Buck/Inverting Switching Regulators](http://www.ti.com/lit/ds/symlink/mc33063a.pdf)
* Schottky Diode: [1N5817](http://www.diodes.com/_files/datasheets/ds23001.pdf)
* Capacitors: 100 uF, Ct=470 pF, Co=470 uF, Cfilter=100 uF 
* Resistors: R1=1.2 kOhm, R2=3.8 kOhm, Rsc=.33 Ohm
* Inductors: L=220 uH, Lfilter=1 uH


### Design Requirements

* Vsat = Saturation voltage of the output switch
* VF = Forward voltage drop of the chosen output rectifier
* Vin = Nominal input voltage
* Vout = Desired output voltage
* Iout = Desired output current
* fmin = Minimum desired output switching frequency at the selected values of Vin and Iout
* Vripple = Desired peak-to-peak output ripple voltage. The ripple voltage directly affects the line and load regulation and, thus, must be considered. In practice, the actual capacitor value should be larger than the calculated value, to account for the capacitor's equivalent series resistance and board layout.

```python
Vsat = ? # VDC - need part
Vf = 0.450 # VDC - 1N5817 datasheet @ 1A
Vin = 24. # VDC
Vout = 5. # VDC
Iout = 1.5 # A
Fmin = 50000 # Hz
Vripple = .010 # VDC

t_on_div_t_off = (v_out + v_f) / (v_in_min - v_sat - v_out)
t_on_plus_t_off = 1./f
Ipk_switch = 
Co =  Ipu_switch * (t_on + t_off)
```
