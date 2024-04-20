
$$\hat{H} (X) = -\sum_{i=1}^c \hat{p_i} * log_2(\hat{p_i})$$

| Features       | Class     |
| -------------- | --------- |
| $x_1=<t,d>$    | $y_1 = +$ |
| $x_2 = <s, d>$ | $y_2 = +$ |
| $x_3 = <t,b>$  | $y_3 = -$ |
| $x_4 = <t,r>$  | $y_4 = -$ |
| $x_5 = <s, b>$ | $y_5 = +$ |

Answer:
Just expand the equation and plug in values. You don't need to compute logarithms
$$H(X) = -\frac{3}{5} * log_2(\frac{3}{5}) -\frac{2}{5} * log_2(\frac{2}{5}) = 0.971 \ \text{bits}$$
