| x |  |
| ---- | ---- |
| 0 | 0 |
| 2 | 0 |
| 1 | 0 |
| 0 | 1 |
|  |  |


| (y) labels |
| ------ |
| 0      |
| 1      |
| 0      |
| 1      |
|        |
With these, the algorithm then has the model: $$y = 0.4\ x_1 + 1\ x_2$$
The '0.4' and the '1' in front of the numbers are the weights in the model, arbitrary in this case.

And this can output simple but correct stuff!
$$0.4 \cdot 0 + 0 = 0$$
$$0.4 \cdot 2 + 0 = 0.8 -> 1$$
$$0.4 \cdot 1 + 0 = 0.4 -> 0$$
$$0.4 \cdot 0 + 1 = 1 -> 1$$
Simple calculations, but correctly finds something about our dataset. How was the algorithm found? Don't worry about that yet, kind of a "blackbox" of sorts.
