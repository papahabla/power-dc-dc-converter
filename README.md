# WORK IN PROGRESS

# Simple DC-DC converters

## 24 V to 5 V @ 3 A

This project will convert a regulated 24 VDC supply to 5 VDC using a switching regulator. Switch regulators
essentually reduce (buck), or boost a DC voltage to supply power to a device needing that specific voltage. 
A common design in a lot of projects requiring parts with different voltage supply levels is to first 
generate regulated power for supplying the part with the highest voltage requirement, and then converting 
that power down to the voltage levels needed by the other parts.


## LM2596

### Design


#### Inductor Selection (L1)

```
Vin = 24. # VDC
Vout = 5. # VDC
Vsat = 1.5 # VDC
Vd = .5 # VDC
Ext = (Vin - Vout - Vsat) * ((Vout + Vd) / (Vin - Vsat + Vd)) * (1000. / 150) # (V * uS)
print(Ext)
```
