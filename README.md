# !!!!!!!!!! WORK IN PROGRESS !!!!!!!!!!!!

# Simple DC-DC converters

## 40 VDC Max Input to 1.2-35 VDC @ 3 A Output

This project will convert a regulated or unregulated 40 VDC supply to an adjustable 1.2-35 VDC using a switching regulator. Switch regulators essentually reduce (buck), or boost a DC voltage to supply power to a device needing that specific voltage. 
A common design in a lot of projects requiring parts with different voltage supply levels is to first 
generate regulated power for supplying the part with the highest voltage requirement, and then converting 
that power down to the voltage levels needed by the other parts.


## LM2596 Switching Regulator

* [Datasheet](http://www.onsemi.com/pub_link/Collateral/LM2596-D.PDF)


### BOM

*As shown in figure 30*
* Cin - 100 uF, 63 V, Aluminium Electrolytic
* Cout - 220 uF, 25 V, Aluminium Electrolytic  
* C1 - 100 uF, 63 V, Aluminium Electrolytic 
* D1 - 3.0 A, 40 V, Schottky Rectifier, 1N5822 
* L1 - [38 uH, PE-54040NL, Pulse Electronics Corporation](http://productfinder.pulseeng.com:8080/files//datasheets/SPM2007_47.pdf)
* L2 - [25 uH, PE-54041NL, Pulse Electronics Corporation](http://productfinder.pulseeng.com:8080/files//datasheets/SPM2007_47.pdf)
* R1 - 1.21 kOhm 0.25 W, 1% metal film resistor
* R2 - 50 kOhm pot
* On/Off Switch

*Delayed Startup Options*
* C2 - .1 uF
* R3 - 47 kOhm


### Design

### Programming Output Voltage

The output voltage is set using two resisotors. Resistor R1 can be between 1.0 k and 5.0 kW. (For best temperature coefficient and stability with time, use 1% metal film resistors).

```python
Vref = 1.23
R2 = 3000.
R1 = 1000.
Vout = Vref * (1.0 + R2 / R1)
```
In order to set a specific output voltage, we start with *R1* within the recomended range(1k to 5k). When selecting an R1 value of 1 kOhm, the value for R2 is calculated for our desired 5 V output as:
```python
Vref = 1.23
Vout = 5.0
R1 = 1000.
R2 = R1 * (Vout / Vref - 1.0)
```

Testing our R1, and R2 values using the equation from above, shows that the R1 and R2 combination will provide the target output voltage:
```python
Vout = Vref * (1.0 + R2 / R1)
```

#### Input Capacitor

If the switching regulator isn't close to a regulated power source, an input bypass capacitor (C1) must be used. If the power source isn't regulated, an input capacitor is basically required.

* 100 uF (low ESR)

#### Inductor Selection (L1)

The following calculates E*T which is used to lookup the recomended inductor in the datasheet. 

```python
Vin = 25. # VDC - Maximum Unregulated Input Voltage
Vout = 5. # VDC - Regulated Output Voltage
Iload = 3. # A - Maximum Load Current
Vsat = 1.5 # VDC
Vd = .5 # VDC
ExT = (Vin - Vout - Vsat) * ((Vout + Vd) / (Vin - Vsat + Vd)) * (1000. / 150) # (V * uS)
print(ExT)
```

#### Catch Diode

* >= 30 V Schottky diod or any fast recovery diode in table 2


#### Output Capacitor

For low output ripple voltage and good stability, low ESR output capacitors are 
recommended. A low ESR value is needed for low output ripple voltage, typically 
1% to 2% of the output voltage. But if the selected capacitor’s ESR is extremely 
low (below 0.05 W), there is a possibility of an unstable feedback loop, 
resulting in oscillation at the output. This situation can occur when a tantalum 
capacitor, that can have a very low ESR, is used as the only output capacitor.

* 470 mF/35 V or 220 mF/35 V

#### Feedforward Capacitor

mainly for higher input voltages.

* 15 nF or 5 nF


