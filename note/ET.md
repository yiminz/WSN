# ETPF

ref: Stochastic Event-Triggered Particle Filtering for State Estimation(2016)



The basic idea behind of event based sampling strategries is that information is transimitted from sensors to processing units only if certain events happen.

ETSE(envent triggered state estimation): systems states are estimated using event-triggered(ET) measurements and although sesnors measure the outputs of the system at each sampling instant, the measurements are sent to the estimator if the triggering condition is satisfied.  In this framework, once the measurements are received by the estimator, it updates the estimaion value and when it is not received, the estimator selects a predefined value. 



The previous works in the literature on ETSE can generally be categorized into two groups: development of novel event-triggering(ET) considitions and development of event-based estimation given a specific ET condition. 

To overcome the problem of costly communication and limitation in energy resources, sensor are equipped with event based data schedulers. A triggering index, $\gamma_k$ is considered to schedule the sensors communication in which, $\gamma_k = 0$ means an ET condition is not satisfied and no measurement is transferred. Once $\gamma_k = 1$ the measurements are transmitted to the estimator.  The stochastic ET strategy is selected as follows:
$$
\gamma_k = \left\{ \begin{aligned}0 & \quad if  \quad \phi(y_k,y_{l_k}) > \theta_k \\
1&\quad otherwise\end{aligned} \right.
$$
where $\phi()$ is a triggering function which determines the information available to the estimator at the no-event instants, $\theta_k$ is also considered as a random variable with a uniform distribution over $[0,1]$ . A stochastic send-on-delta with a Gaussian Kernel is considered in this paper as follows
$$
\phi(y_k,y_{l_k}) = exp(-\frac{1}{2} (y_k - y_{l_k})\Sigma(y_k - y_{l_k})^T
$$
where $\Sigma$ is a non-singular positive dent weighting matrix that determines the shape of the Gaussian Kernel. $y_{l_k}$ is the measurement vector sent by the sensor at the time instant $l_k$ which is the last information received by the estimator. 



The measurement information received by the estimator is denoted as follows:
$$
Y_k = \left\{
\begin{aligned}
y_k & \quad \gamma_k = 1 \\
Y_k & \quad \gamma_k = 0
\end{aligned}
\right.
$$

## ET PF

In the first case, ET condition is not satisfied and thus the measurements are not received by the estimator. In the second case, the ET condition is satisfied and the estimator receives the current measurements.

**First Case**

Using the Bayesian rule, it follows that
$$
p(x_k|I_k) = p(x_k|\gamma_k =0,I_{k-1})=\frac{p(\gamma_k = 0|x_k,I_{k-1})}{p(\gamma_k=0|I_{k-1})}p(x_k|I_{k-1})
$$

$$
p(x_k|I_{k-1})=\frac{1}{N}\sum_{i=1}^N p(x_k|x_{k-1}^{i+},I_{k-1})
$$


$p(x_k|x_{k-1}^{i+},I_{k-1})$ is approximated by $\delta(x_k - x_k^{i-})$ which yields:


$$
p(x_k|I_{k-1}) \sim \frac{1}{N}\sum \delta(x_k - x_k^{i-})\\
p(x_k|I_{k}) \sim \frac{1}{N}\sum w_k^i\delta(x_k - x_k^{i-})\\
$$
where $w_k^i$ is the weight corresponding to the $i-$th particle.

**Second Case**


