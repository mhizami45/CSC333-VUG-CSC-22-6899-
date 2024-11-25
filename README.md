# CSC333-VUG-CSC-22-6899-
import numpy as np
import matplotlib.pyplot as plt
from scipy.optimize import linprog

# Define constraints
x = np.linspace(0, 10, 400)
y1 = (12 - 2*x) / 3
y2 = (8 - x) / 2

# Feasible region shading
plt.figure(figsize=(8, 6))
plt.plot(x, y1, label='2A + 3B = 12')
plt.plot(x, y2, label='A + 2B = 8')
plt.fill_between(x, np.minimum(y1, y2), 0, where=(np.minimum(y1, y2) >= 0), color='gray', alpha=0.3)

# Labels and legend
plt.title("Graphical Solution for Problem 1")
plt.xlabel("A (Product A)")
plt.ylabel("B (Product B)")
plt.legend()
plt.xlim(0, 10)
plt.ylim(0, 10)
plt.grid()
plt.show()

# Optimization
c = [-3, -4]  # Objective function coefficients (maximize becomes minimize with negative)
A = [[2, 3], [1, 2]]  # Coefficients for inequalities
b = [12, 8]  # RHS of inequalities
result = linprog(c, A_ub=A, b_ub=b, bounds=(0, None), method='highs')

print("Optimal Solution:")
print(f"A = {result.x[0]:.2f}, B = {result.x[1]:.2f}")
print(f"Maximum Profit = {(-result.fun):.2f}")
