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

As shown in the tuning process, these three kinds of error do have the effects. 

increase the absolute value of the Kp, would dramatically drive back to target, however to large value would lead to overshot and oslation

increase the absolute value of the Ki, would prevent some systemic control errors. which cannot reflect in this project. however it is nessacary in reality

increase the absolute value of the Kd, would reduce the overshot, and ease oslation. however, make the correction less powerful. 
This is why the increase the Kd, make the turns not good

## Describe how the final hyperparameters were chosen
The final hyperparameters were tuned manually.
Kp, Ki, Kd

notice the cte number and the cte changes. 


(1, 0, 0)
oppersite

(-1, 0, 0)
oscillation

(-0.1, 0, 0)
oscillation less, more oscillation at turns.

(-0.1, 0, 1)
oscillation a little more, not good at turns.

(-0.1, 0, -1)
became stable, but not good at turns. 
need increase the Kp

(-0.2, 0, -1)
turn is better, but oscillation more

notice the change of the cte, ~ 0.04. 10^-2 
so would like to change 

(-0.2, 0, -5)
decent 

(-0.2, -0.1, -5)
bad
(-0.2, -0.01, -5)
bad oscilation
(-0.2, -0.001, -5)
oscilation smaller

(-0.2, -0.0001, -5)
OK
(-0.2, -0.00001, -5)
OK

no dramatic improvement from (-0.2, 0, -5)







