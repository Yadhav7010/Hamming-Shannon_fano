# Huffman-Shannon_fano
# Aim:
Consider a discrete memoryless source with symbols and statistics {0.125, 0.0625, 0.25, 0.0625, 0.125, 0.125, 0.25} for its output. 
Apply the Huffman and Shannon-Fano to this source. 
Show that by drawing the tree diagram, and 
Calculate the average code word length, entropy, variance, redundancy, and efficiency.
# Tools Required:
Python IDE with Numpy and Scipy.
# Program:
```
import heapq
import math

p = [0.4, 0.19, 0.16, 0.15, 0.15]

# Create min heap
heap = [[weight, [symbol, ""]] for symbol, weight in enumerate(p)]
heapq.heapify(heap)

while len(heap) > 1:
    lo = heapq.heappop(heap)
    hi = heapq.heappop(heap)
    for pair in lo[1:]:
        pair[1] = '0' + pair[1]
    for pair in hi[1:]:
        pair[1] = '1' + pair[1]
    heapq.heappush(heap, [lo[0] + hi[0]] + lo[1:] + hi[1:])

huffman_codes = sorted(heap[0][1:], key=lambda x: x[0])

# Extract lengths
lk = [len(code[1]) for code in huffman_codes]

# Calculations
L = sum(p[i] * lk[i] for i in range(len(p)))
H = sum(p[i] * math.log2(1/p[i]) for i in range(len(p)))
eff = H / L
red = 1 - eff
var = sum(p[i] * (lk[i] - L)**2 for i in range(len(p)))
print("Probability:", p)
print("Code lengths:", lk)
print("Average Length:", round(L,3))
print("Entropy:", round(H,3))
print("Efficiency:", round(eff,3))
print("Redundancy:", round(red,3))
print("Variance:", round(var,3))
 
```
# Calculation:

![WhatsApp Image 2026-02-16 at 8 40 54 PM](https://github.com/user-attachments/assets/34083359-84c0-40dd-92e7-7819d1639058)
![WhatsApp Image 2026-02-16 at 8 40 54 PM (1)](https://github.com/user-attachments/assets/798652d3-3d21-4043-95f3-65c48f31774f)

# Output

<img width="1636" height="725" alt="image" src="https://github.com/user-attachments/assets/5adb1aa9-624d-4cb5-a5ff-9107cb0b44e2" />

# Results:
The Huffman and Shannon-Fano of the given statistics {0.125, 0.0625, 0.25, 0.0625, 0.125, 0.125, 0.25} using python are verified.
