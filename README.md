# END3.0-Session2

TSAI Assignment: Sunny Manchanda

Assignment 2 on Backpropogation

Assignment:

1. Rewrite the whole excel sheet showing backpropagation. Explain each major step, and write it on Github. 

i. Use exactly the same values for all variables as used in the class

ii. Take a screenshot, and show that screenshot in the readme file

iii. Excel file must be there for us to cross-check the image shown on readme (no image = no score)

iv. Explain each major step

v. Show what happens to the error graph when you change the learning rate from [0.1, 0.2, 0.5, 0.8, 1.0, 2.0] 

2. Submit the GitHub link. Github link must be public (check the link without logging in, if it opens, then only share the link as an assignment). 


Excel Sheet Link: https://github.com/reseach/-END3.0-Session2/blob/main/END3-Session2.xlsx

Screenshot:

![image](https://user-images.githubusercontent.com/91345062/135693503-d184ebaf-1f6a-41ff-ba65-c1c5b791aebc.png)

Loss Cureve:

![image](https://user-images.githubusercontent.com/91345062/135693625-5d89d021-046b-412a-9351-6d88c914b14e.png)

We observe that increase in lthe learning rate increases the rate at which the network learns.

Major Steps:

Network Architecture:
<img width="574" alt="NN" src="https://user-images.githubusercontent.com/91345062/135693870-6f5f9634-a26a-447a-b624-4ca879e842bd.png">

**Forward Propogation:
**
The forward pass through the neural network is as per the network architecture:

>
For Node h1,

  h1 = i1*w1 + i2*w2

For Node h2,

  h2 = i1*w3 + i2*w4

Activation Function on the Node h1, out_h1

  out_h1 = σ(h1) =  1/(1+exp(-h1))

Activation Function on the Node h2, out_h2

  out_h2 = σ(h2) =  1/(1+exp(-h2))

Node o1,

  o1 = out_h1*w5 + out_h2*w6

Node o2,

  o2 = out_h1*w7 + out_h2*w8

Activation Function on the Node o1, out_o1

  out_o1 = σ(o1) =  1/(1+exp(-o1))

Activation Function on the Node o2, out_o2

  out_o2 = σ(o2) =  1/(1+exp(-o2))

Error at the output node out_o1, E1

  E1 = 1/2 * (t1 - out_o1)2  (Mean Square Error)

Error at the output node out_o2, E2

  E2 = 1/2 * (t2 - out_o2)2  (Mean Square Error)


**Backward Propogation:
**

The expected error for out_o1 and out_o2 is t1 and t2 respectively.

Total Error at the Output Node,

Total error wrt w5:

∂E_Total/∂w5 = ∂(E1 + E2)/∂w5 = ∂E1/∂w5 =  ∂E1/out_o1*∂out_o1/o1*∂o1/∂w5 (By chain rule)

Total error of E1 wrt out_o1:

∂E1/∂out_o1 = out_o1 - t1

Total error of out_o1 wrt o1:

∂out_o1/∂o1 =  σ(o1)* (1 - σ(o1)) = out_o1*(1-out_o1)

Total error of o1 wrt w5:

∂o1/∂w5 = out_h1

Total error, E_total wrt w5:

∂E_Total/∂w5 = (out_01 - t1) * out_o1*(1-out_o1)*out_h1

Similarly, Total error, E_total wrt w6, w7 and w8:

∂E_Total/∂w6 = (out_01 - t1) * out_o1*(1-out_o1)*out_h2

∂E_Total/∂w7 = (out_02 - t2) * out_o2*(1-out_o2)*out_h1

∂E_Total/∂w8 = (out_02 - t2) * out_o2*(1-out_o2)*out_h2
 
∂E_total/∂out_h1 = ∂(E1  +E2)/ ∂out_h1 

∂E1/∂out_h1 = ∂E1/out_o1*∂out_o1/∂o1*∂o1/∂out_h1

∂E1/∂out_h2 = ∂E1/out_o1*∂out_o1/∂o1*∂o1/∂out_h2

∂E2/∂out_h1 = ∂E2/out_o2*∂out_o2/∂o2*∂o2/∂out_h1

∂E_Total/∂out_h1 = (out_o1 - T1) * out_o1 * (1 - out_01) * w5 + (out_o2 - t2)*out_o2*(1-out_o2)*w7

∂E_Total/∂out_h2 = (out_o1 - T1) * out_o1 * (1 - out_01) * w6 + (out_o2 - t2)*out_o2*(1-out_o2)*w8


**Total error, E_total wrt w1 to w8:
**

∂E_Total/∂w1 = ∂E_Total/∂out_h1*∂out_h1/∂h1*∂h1/w1

∂E_Total/∂w1 = ∂E_Total/∂out_h1*out_h1*(1-out_h1)*i1

∂E_Total/∂w2 = ∂E_Total/∂out_h1*out_h1*(1-out_h1)*i2

∂E_Total/∂w3 = ∂E_Total/∂out_h2*out_h2*(1-out_h2)*i1

∂E_Total/∂w4 = ∂E_Total/∂out_h2*out_h2*(1-out_h2)*i2

∂E_Total/∂w5 = (out_01 - t1) * out_o1*(1-out_o1)*out_h1

∂E_Total/∂w6 = (out_01 - t1) * out_o1*(1-out_o1)*out_h2

∂E_Total/∂w7 = (out_02 - t2) * out_o2*(1-out_o2)*out_h1

∂E_Total/∂w8 = (out_02 - t2) * out_o2*(1-out_o2)*out_h2

The weights are then update using the gradient step:

wi = wi - learning_rate * ∂E_Total/∂wi



