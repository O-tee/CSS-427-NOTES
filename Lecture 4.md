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
<br/>

Lower Level Calibration 
- If the sensor is not linear, we can force it.
  - Polynomial:
    - x(t) = a5 t5 + a4 t4+ a3 t3 + a2 t2 + a1 t + a0
- This extrapolates poorly!
- Usually dominated by a1 and a0.
- Higher order terms smooth out the bumps.
- Rational: x(t) = (a t + b) / (t + d)
  - Better extrapolation and easier to invert.
<br/>

Electronic and Microcontroller Symbols 
<img width="1039" alt="image" src="https://github.com/user-attachments/assets/15c12d25-2f2b-4cc9-b698-9db76dc0a33e" />
<br/>

Fuses
- If the current gets too high, it generates a lot of heat and burns out the resistor or IC.
- Circuits are usually designed with sacrificial elements called fuses. 
- The fuse will be destroyed with too much current, but it protects the rest of the circuit. 
- A fuse can be made from a thin piece of metal that vaporizes with too much current. 
- Fuses are rated for their maximum current. 
- There are fast-blow fuses that go right away at the stated current and slow-blow fuses that wait for the excess current to be sustained.




