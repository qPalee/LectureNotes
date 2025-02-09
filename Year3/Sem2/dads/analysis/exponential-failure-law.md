# The Exponential Failure Law
A way of making generalised assumptions to allow modelling

### Reliability
Reliability of a system is the probability the system delivers correct services over a specified time period under given conditions

More detail available at [[attributes]]
### Failure Rate
Failure rate is the expected number of failures of a device over a given time frame

Typical evolution of failure rate over the lifetime of a system is illustrated by the bathtub curve

![[Pasted image 20250206093642.png]]

This curve has three phases; infant mortality, useful life and wear out

During the useful life of the system, the failure rate function $z(t)$ is assumed to be constant $\lambda$

'If a lightbulb lasts more than 10 hours, it's going to last a long time'
#### Calculating Failure Rate

$U(t)$ is the number of devices running at time $t$
$F(t)$ is the number of failed devices at time $t$

To calculate the reliability of a component over time period ($t_1, t$)
$$Reliability = R(t) = \frac{U(t)}{N}$$
Unreliability is just $1 - R(t)$

### Exponential Failure Law
The exponential failure law: $R(t) = e^{-\lambda t}$

This can only be used when failure rate is constant

It is important to analyse the purpose and usefulness of this

Allows us to plot a graph of reliability vs time as well as analysing the reliability of the device

Since reliability is defined over a specified time period, if reliability drops below a threshold it can be detected

### Reliability Modelling
#### MTTF
Mean Time to Failure

Expected time a system will operate before first failure

If there are $N$ identical systems which run correctly at $t=0$ but they all fail at time $t_0$ then MTTF has the formula
$$MTTF=\sum^{N}_{i=1}\frac{t_i}{N}$$
In the continuous case, MTTF can be calculated using 
$$MTTF=\int^{\infty}_{\infty}t \ f(t) \ dt$$ where $f(t)$ is the failure density function - derivative of unreliability

In the case of $\lambda$, this can be reduced down to $$MTTF=\frac{1}{\lambda}$$
#### MTTR
Mean Time to Repair

MTTR is the average time to repair a failed computer system
Includes time for detecting and locating the fault, repairing it and reconfiguring the system

It can be difficult to predict analytically
- might require experimental measurement for computation

The repair rate is denoted by $\mu$ 
$$MTTR =\frac{1}{\mu}$$

#### MTBF
Mean Time Between Failures

Average time elapsed between failures

It is assumed that after repair, the system works as it was before failure
$$MTBF = MTTR + MTTF$$
