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

Correspondingly, **Kp, Ki, and Kd are proportional gain, integral gain, and derivative gain.** 
They are the parameters to be tuned.

As shown in the following tuning process:

* Increasing the absolute value of the Kp, would drive the vehical back to target point quicker, however if the Kp is too large, it would lead to overshoot and oscillation.

* Increasing the absolute value of the Ki, would prevent steady-state error. If the Ki is too large, the vehical will also oscillate. And the value of Ki should be pretty small. The importance of the Ki is not presented in this project, however it is necessary in real world controller projects.

* Increasing the absolute value of the Kd, would reduce the overshoot, and ease oscillation, at the same time, it will make the correction less powerful. This is the reason why increasing the Kd too much will harm the turning ability of the vehicle.

These observations indeed agree with the characteristics of the three PID controller parameters.

## Describe how the final hyperparameters were chosen
The final hyperparameters (Kp, Ki, Kd) were tuned manually.

* **Step1**: make sure the signs of the parameters. Usually, the three parameters are positive. However, depend on the implemention of the errors, these parameters are negative.
+ Tried (Kp = 1, Ki = 0, Kd = 0), the vehicle went directly off track. which means the parameters should be negative.

* **Step2**: Start with Kp, which is the mean driving force for the controller.
+ Tried (Kp = -1, Ki = 0, Kd = 0), the vehicle start oscillation, and got worse while went further down track.
+ Also notice that the absolute value of the starting "cte" is about 7, then the Kp should be reduced.
+ Tried (Kp = -0.1, Ki = 0, Kd = 0), the vehicle oscillate less, however, the vehicle cannot pass the turn.  


* **Step2**: also adjusting Kd, which can smooth the process.
+ Tried (Kp = -0.1, Ki = 0, Kd = -1), the vehicle became stable, however, the vehicle would on the edges of the track during turns.  
+ Tried (Kp = -0.2, Ki = 0, Kd = -1), the vehicle turns better but osillate more.  
+ Notice that the change the "cte" is at about the levels of 0.05, then decided to increase Kd more.
+ Tried (Kp = -0.2, Ki = 0, Kd = -5), the vehicle had decent performance.  This values were chosen as the final values for the hyperparameters.


* **Step3**: experimenting Ki, which is relate to steady-state error.
+ Tried (Kp = -0.2, Ki = 0.1, Kd = -5), and it is a disaster. The Ki should be very small.
+ Tried (Kp = -0.2, Ki = 0.01, Kd = -5), and it is still a disaster.
+ Tried (Kp = -0.2, Ki = 0.001, Kd = -5), tnd the vehicle oscilate less.
+ Tried (Kp = -0.2, Ki = 0.0001, Kd = -5) and  (Kp = -0.2, Ki = 0.00001, Kd = -5). Under these values, the vehicle can finish the track, but there are no obvious improvements. So (Kp = -0.2, Ki = 0, Kd = -5) were chosen as the final values.
