# Differential Power Analysis
Basically the same as the timing attack

### S-Box lookup
- S-Box is constant time
- Power consumption at the correct clock cycle depends on the output $B_0$
- If we measure this power consumption, we can recover $k[0]$

Similar to the timing attack, we will
- focus on a single key byte
- go over all 256 candidates for that byte
- go over many (x, p(t)) pairs

For each key candidate k, we check if MSBIT($B_0$) == 1 || MSBIT($B_0$) = 0