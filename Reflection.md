## Describe the effect each of the P, I, D components had in your implementation.
Student describes the effect of the P, I, D component of the PID algorithm in their implementation. Is it what you expected?
In the file: PID.cpp, line 19 - 21 are the three kind of errors in PID algorithm
```c++
d_error_ = cte - p_error_;
p_error_ = cte;
i_error_ += cte;
```

 proportional, integral, and derivative



## Describe how the final hyperparameters were chosen
Student discusses how they chose the final hyperparameters (P, I, D coefficients). This could be have been done through manual tuning, twiddle, SGD, or something else, or a combination!
cte


The final hyperparameters were tuned manually.
Kp, Ki, Kd
