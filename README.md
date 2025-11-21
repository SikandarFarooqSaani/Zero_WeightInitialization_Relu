# Zero_WeightInitialization_Relu
# Zero Initialization of Weights in ReLU Networks & Its Consequences  
Using U-Shape Dataset

This experiment demonstrates why **zero (or same-value) weight initialization** is harmful even when using **ReLU activation**, leading to symmetry problems and underfitting.

---

## 📌 Dataset  
- U-shape dataset (used previously).  
- Dataset stored in the repo.  
- Scatter plot created (Image 1 attached) clearly showing a non-linear pattern.
<img width="380" height="248" alt="reluinit1" src="https://github.com/user-attachments/assets/dea8febc-c178-452f-8c5a-a00451ac808c" />

---

## 🧠 Model Setup  
- Simple neural network:
  - **Input layer:** 2 neurons  
  - **Output layer:** 1 neuron  
  - Activation: ReLU (or linear at output depending on dataset)

- After building model:
  - Fetched all model weights
  - **Manually set all weights to 0.5**  
    (This is equivalent to zero-initialization in terms of symmetry.)

- Model compiled and trained for **100 epochs**.

---

## 📉 Observations

### **1. Accuracy Remains Stuck at 0.5**
- The model fails to learn beyond chance level.
- Since all neurons start with the exact same weight:
  - They produce **identical outputs**
  - They receive **identical gradients**
  - They update **in the same direction**, maintaining symmetry  
  → The network behaves like **a single neuron**.

---

### **2. Decision Boundary Stays Linear**
- Even though the U-shape requires a **non-linear boundary**,  
  the model outputs a **straight line**.
- Decision boundary plot (Image 2 attached) confirms this:
- <img width="370" height="248" alt="reluinit2" src="https://github.com/user-attachments/assets/dc16fda2-67ed-4aac-a7f5-26004a3922fc" />

  - No curvature  
  - No separation matching the real pattern  
  → Clear **underfitting**.

---

## ⚠️ Why Does ReLU Also Fail with Zero / Same Weight Initialization?

Even though ReLU is better than sigmoid for avoiding vanishing gradients, it still suffers from **symmetry breaking problems**:

### ❌ **ReLU neurons initialized with same weights behave identically**
- Same input → same output  
- Same gradient → same update  
- Network collapses to a **single linear unit**

### ❌ **No non-linearity is introduced**
- To get a true ReLU non-linear boundary, neurons must learn different slopes.
- With equal initialization, all slopes remain the same.

### ❌ **Model cannot capture any complex pattern**
- ReLU **does not fix symmetry**  
- Initialization must break symmetry (random small weights required)

---

## 🧨 Summary of Consequences

| Problem | Effect |
|--------|--------|
| All weights = same value | Neurons become identical |
| Symmetry not broken | Network acts as 1 neuron |
| ReLU outputs identical values | No non-linear representation learned |
| Accuracy stuck | ~0.5 |
| Decision boundary | Straight line (underfit) |
| Learned function | Always linear |

---

## ✅ Final Conclusion
Zero or same-value weight initialization (0, 0.5, etc.) with **ReLU** causes:

- Neuron symmetry  
- No non-linear modeling  
- Flat / linear decision boundaries  
- Completely **underfitted** models  
- Accuracy stuck at chance levels  

To avoid this, we should always use **random weight initialization** (He initialization for ReLU).

---

