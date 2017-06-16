## Describe the effect each of the P, I, D components had in your implementation.
In the file: PID.cpp, line 19 - 21 are the three kind of errors in PID algorithm
```c++
d_error_ = cte - p_error_;
p_error_ = cte;
i_error_ += cte;
```
P error is the proportional, main error
I error is the integral, prevent systemic error
D error is the derivative, prevent overshot



## Describe how the final hyperparameters were chosen
The final hyperparameters were tuned manually.
Kp, Ki, Kd

notice the cte number and the cte changes. 



