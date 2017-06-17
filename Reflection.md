## Describe the effect each of the P, I, D components had in your implementation.
In the file: PID.cpp, line 19 - 21 are the three kind of errors in PID algorithm
``` cpp
d_error_ = cte - p_error_;
p_error_ = cte;
i_error_ += cte;
```
And, on line 25, there is the equation for return total error.
``` cpp
return Kp_ * p_error_ + Ki_ * i_error_ + Kd_ * d_error_; 
```

**P error** is the **proportional error**, which is used to generate the he main correction force.
The larger the cte, the larger the P error, hence there will be larger correction force.

**I error** is the **integral error**, which is the sum of previous errors (or recent errors depend on implementation).
This error is used to prevent systematic control error, or called steady-state error.

**D error** is the **derivative error**, is the rate of the error changing. 
Here, we simplify it with the change of the errors between two time points.
This error is used to smooth the correction process, and prevent overshoot.

Correspondingly, Kp, Ki, and Kd are proportional gain, integral gain, and derivative gain. They are the parameters to be tuned.

As shown in the following tuning process:

*** increase the absolute value of the Kp, would dramatically drive back to target, however to large value would lead to overshot and oslation

*** increase the absolute value of the Ki, would prevent some systemic control errors. which cannot reflect in this project. however it is nessacary in reality

*** increase the absolute value of the Kd, would reduce the overshot, and ease oslation. however, make the correction less powerful. 
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







