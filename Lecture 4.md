# Lecture 4 (4/8/25) Sensors Electronics.ppxt

## Things I'm confused about 

## Something to read after the lecture 

## Notes  

When tested at 25°C, the TMP36 typically is accurate to ±1°C, but it can be off by ±3°C
- scale factor is typically 10 mV/°C
- scale factor typically remains linear within 0.5°C
- When held at 150°C for 1000 hours, the sensor usually varies by 0.4°C or less.
- Output voltage is limited to 0.1 to 2V, corresponding to a temperature range of -40 to 150 °C (-40 to 302°F) 
<br/>

Calibration
- Linear: f(t) = a * t
- Affine: f(t) = a * t + b
- More general affine: f(t) = a * x(t) + b
- What is x(t)?
  - For the TMP36, f(x) = 100 (5/1023) * x + (-50)
    - f(x) = 0.489 * x - 50 
  - Here x is the reading we get from Arduino: 0 to 1023f(x) is temperature in C.






