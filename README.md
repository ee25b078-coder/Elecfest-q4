# Elecfest-q4
## 1. Deriving Transfer function(H(s)) for given RC Lowpass Filter

### Circuit Definition
* **Input:** $v_{in}(t)$
* **Output:** $v_{out}(t)$ (taken across the capacitor)
* **Current:** $i(t)$ through the series loop

### Time-Domain Differential Equation
By Kirchhoff's Voltage Law (KVL), the sum of voltage drops equals the input voltage:
$$v_{in}(t) = v_R(t) + v_C(t)$$

Substituting the component laws ($v_R = iR$ and $i = C \frac{dv_C}{dt}$) and knowing $v_C(t) = v_{out}(t)$:
$$v_{in}(t) = R \left( C \frac{dv_{out}(t)}{dt} \right) + v_{out}(t)$$

This yields the first-order linear ordinary differential equation (ODE):
$$v_{in}(t) = RC \frac{dv_{out}(t)}{dt} + v_{out}(t)$$

### S-Domain Transfer Function
Apply the Laplace transform, assuming zero initial conditions ($v_{out}(0) = 0$):
$$V_{in}(s) = RC(sV_{out}(s)) + V_{out}(s)$$

Factor out $V_{out}(s)$ and solve for the transfer function $H(s) = \frac{V_{out}(s)}{V_{in}(s)}$:
$$V_{in}(s) = V_{out}(s)(sRC + 1)$$
$$H(s) = \frac{1}{sRC + 1}$$

### Applied Values
Given $R = 500\,\Omega$ and $C = 50\,\mu\text{F}$:
$$RC = 500 \cdot (50 \times 10^{-6}) = 0.025\,\text{s}$$
$$H(s) = \frac{1}{0.025s + 1}$$

---

## 2. Deriving H(s) for the Band Pass filter

### Circuit Definition
* **Input:** $v_{in}(t)$
* **Output:** $v_{out}(t)$ (taken across $C_2$)
* **Intermediate Node:** $v_x(t)$ (between $C_1$, $R_1$, and $R_2$)

### Time-Domain Differential Equations
Applying Kirchhoff's Current Law (KCL) at node $v_x$:
$$C_1 \frac{d(v_{in}(t) - v_x(t))}{dt} = \frac{v_x(t)}{R_1} + \frac{v_x(t) - v_{out}(t)}{R_2}$$

Applying KCL at node $v_{out}$:
$$\frac{v_x(t) - v_{out}(t)}{R_2} = C_2 \frac{dv_{out}(t)}{dt}$$

Isolate $v_x(t)$ from the second equation:
$$v_x(t) = v_{out}(t) + R_2 C_2 \frac{dv_{out}(t)}{dt}$$

Differentiate $v_x(t)$ with respect to time:
$$\frac{dv_x(t)}{dt} = \frac{dv_{out}(t)}{dt} + R_2 C_2 \frac{d^2v_{out}(t)}{dt^2}$$

Substitute $v_x(t)$ and its derivative into the first KCL equation, and multiply by $R_1$:
$$R_1 C_1 \frac{dv_{in}(t)}{dt} - R_1 C_1 \left( \frac{dv_{out}(t)}{dt} + R_2 C_2 \frac{d^2v_{out}(t)}{dt^2} \right) = v_{out}(t) + R_2 C_2 \frac{dv_{out}(t)}{dt} + R_1 C_2 \frac{dv_{out}(t)}{dt}$$

Rearranging yields the second-order ODE:
$$R_1 R_2 C_1 C_2 \frac{d^2v_{out}(t)}{dt^2} + (R_1 C_1 + R_2 C_2 + R_1 C_2) \frac{dv_{out}(t)}{dt} + v_{out}(t) = R_1 C_1 \frac{dv_{in}(t)}{dt}$$

### S-Domain Transfer Function
Apply the Laplace transform assuming zero initial conditions:
$$R_1 R_2 C_1 C_2 s^2 V_{out}(s) + (R_1 C_1 + R_2 C_2 + R_1 C_2) s V_{out}(s) + V_{out}(s) = R_1 C_1 s V_{in}(s)$$

Factor out $V_{out}(s)$ to find the ratio $H(s)$:
$$V_{out}(s) \left[ s^2 (R_1 R_2 C_1 C_2) + s (R_1 C_1 + R_2 C_2 + R_1 C_2) + 1 \right] = V_{in}(s) (s R_1 C_1)$$

$$H(s) = \frac{s R_1 C_1}{s^2 (R_1 R_2 C_1 C_2) + s (R_1 C_1 + R_2 C_2 + R_1 C_2) + 1}$$

### Applied Values
Given $R_1 = R_2 = 1.6\,\text{k}\Omega$ and $C_1 = C_2 = 10\,\text{nF}$:
* $R_1 C_1 = R_2 C_2 = R_1 C_2 = 1.6 \times 10^{-5}\,\text{s}$
* **$s^2$ coefficient:** $(1.6 \times 10^{-5})^2 = 2.56 \times 10^{-10}\,\text{s}^2$
* **$s$ coefficient:** $3 \cdot (1.6 \times 10^{-5}) = 4.8 \times 10^{-5}\,\text{s}$

$$H(s) = \frac{1.6 \times 10^{-5} s}{2.56 \times 10^{-10} s^2 + 4.8 \times 10^{-5} s + 1}$$
