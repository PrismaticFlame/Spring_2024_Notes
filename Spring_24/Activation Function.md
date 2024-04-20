Activation functions play a crucial role in artificial neural networks by introducing non-linearities into the model. These non-linearities allow neural networks to learn complex relationships in data, enabling them to approximate a wide range of functions. In the context of neural networks, activation functions determine the output of a neuron or a layer of neurons, influencing the information flow through the network.

Here are some commonly used activation functions:

### 1. **Sigmoid Function:**
   - **Mathematical Form:**
     $\sigma(x) = \frac{1}{1 + e^{-x}}$
   - **Range:**
     $0 \leq \sigma(x) \leq 1$
   - **Properties:**
     - S-shaped curve that squashes input values to the range [0, 1].
     - Commonly used in the output layer of binary classification models.
     - Suffers from the vanishing gradient problem for very large or very small input values.

### 2. **Hyperbolic Tangent (tanh) Function:**
   - **Mathematical Form:**
     $\tanh(x) = \frac{e^{2x} - 1}{e^{2x} + 1}$
   - **Range:**
     $-1 \leq \tanh(x) \leq 1$
   - **Properties:**
     - Similar to the sigmoid but with a range of [-1, 1].
     - Suitable for output layers in models where the target values are in the range [-1, 1].
     - Still suffers from the vanishing gradient problem.

### 3. **Rectified Linear Unit (ReLU):**
   - **Mathematical Form:**
     $\text{ReLU}(x) = \max(0, x)$
   - **Range:**
     $0 \leq \text{ReLU}(x)$
   - **Properties:**
     - Simple and computationally efficient.
     - Widely used in hidden layers of neural networks.
     - Addresses the vanishing gradient problem for positive input values.
     - However, it can suffer from the "dying ReLU" problem where neurons may become inactive during training.

### 4. **Leaky ReLU:**
   - **Mathematical Form:**
     $\text{Leaky ReLU}(x) = \max(\alpha x, x)$
   - **Range:**
     $-\infty \leq \text{Leaky ReLU}(x) \leq \infty$
   - **Properties:**
     - Similar to ReLU but allows a small, non-zero gradient for negative input values (\(\alpha\) is a small positive constant).
     - Intended to address the "dying ReLU" problem.

### 5. **Parametric ReLU (PReLU):**
   - **Mathematical Form:**
     $\text{PReLU}(x) = \max(\alpha x, x)$
   - **Range:**
     $-\infty \leq \text{PReLU}(x) \leq \infty$
   - **Properties:**
     - Extension of Leaky ReLU where \(\alpha\) is learned during training.
     - Allows the network to adaptively learn the best value for \(\alpha\).

### 6. **Sigmoid and Hyperbolic Tangent for Gradients:**
   - Sometimes used in the context of gradients during backpropagation.
   - **Softmax Function:** Used in the output layer of a neural network for multi-class classification tasks. It converts raw scores (logits) into probabilities.

### 7. **Gated Activation Functions:**
   - **Gated Recurrent Unit (GRU) and Long Short-Term Memory (LSTM):**
     - Specialized activation functions used in recurrent neural networks (RNNs) to capture and propagate information across sequences effectively.

### 8. **Swish Activation:**
   - **Mathematical Form:**
     $\text{Swish}(x) = x \cdot \sigma(x)$
   - **Properties:**
     - Proposed as a self-gated activation function.
     - Empirically found to perform well in deep networks.

### 9. **Exponential Linear Unit (ELU):**
   - **Mathematical Form:**
     $\text{ELU}(x) = \begin{cases} x & \text{if } x > 0 \\ \alpha (e^x - 1) & \text{if } x \leq 0 \end{cases}$
   - **Range:**
     \[ -\alpha \leq \text{ELU}(x) \leq \infty \]
   - **Properties:**
     - Similar to ReLU but allows a small negative output for negative input values.

### 10. **Softmax Activation:**
   - **Mathematical Form (for \(K\) classes):**
     $\text{Softmax}(x)_i = \frac{e^{x_i}}{\sum_{j=1}^{K} e^{x_j}}$
   - **Range:**
     $0 \leq \text{Softmax}(x)_i \leq 1$
   - **Properties:**
     - Converts raw scores (logits) into a probability distribution over multiple classes.

### Choosing an Activation Function:

- **Sigmoid or

 **Hyperbolic Tangent:**
  - Often used in the output layer for binary classification tasks.
  - Suitable for tasks where the output needs to be in a bounded range.

- **ReLU and Its Variants:**
  - Commonly used in hidden layers due to simplicity and efficiency.
  - ReLU variants like Leaky ReLU or Parametric ReLU are employed to address certain issues.

- **Softmax:**
  - Applied to the output layer for multi-class classification problems.

- **Gated Activation Functions (GRU, LSTM):**
  - Used in recurrent neural networks to capture long-term dependencies in sequential data.

- **Task-Specific Considerations:**
  - The choice of activation function may depend on the specific characteristics of the task and the data.

### Example (Python - TensorFlow/Keras):

```python
import tensorflow as tf
from tensorflow.keras.layers import Dense, Activation

# Example neural network model using ReLU activation in hidden layers
model = tf.keras.Sequential([
    Dense(128, input_shape=(input_size,), activation='relu'),
    Dense(64, activation='relu'),
    Dense(output_size, activation='softmax')
])
```

In this example, a simple neural network model is created using the TensorFlow/Keras library. The ReLU activation function is used in the hidden layers, and softmax activation is used in the output layer for a multi-class classification task. The choice of activation functions may vary based on the specific requirements of the task and the characteristics of the data.