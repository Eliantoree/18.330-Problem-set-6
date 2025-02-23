# 18.330-Problem-set-6
18.330 Problem set 6

**Download Link:https://programming.engineering/product/18-330-problem-set-6/**

Description
5/5 – (2 votes)
Exercise 1: Runge–Kutta methods

Consider a Runge–Kutta method starting at ( , ) that takes an Euler step of length /2 to ( +1/2, +1/2) and then uses the new evaluation at that point to take a complete Euler step from ( , ) of length ℎ.

Find the order of this method and write down its Butcher tableau. We will refer to it as the “midpoint method”.

Define a type RKMethod to represent a general explicit Runge–Kutta method defined by a Butcher tableau as follows:

struct RKMethod{T}

c::Vector{T}

b::Vector{T}

a::Matrix{T}

s::Int # number of stages

end

Make it into a function by completing the function

function (method::RKMethod)(f, x, t, h)

…

end

to execute one step of the corresponding Runge–Kutta method with initial condition at time and step size ℎ. Your code should work for both scalar and vector and a possibly vector-valued function = ( , ) (Assume that is a lower-triangular matrix, corresponding to an explicit method.)

Define RK methods euler, midpoint and RK4 using their respective tableaus.

Write a routine integrate with the signature

function integrate(method, f, x0, t0, t_final, h)

where method is a RK method as defined above and ℎ is a fixed step size.

Make sure that the final step lands exactly at the final time by taking that final step as a special case.

Use each method on the ODE ̇ = 1.5 with 0 = 2 and integrate from = 0 for a time final = 3.

Find the rate of convergence of the numerical solution to the exact solu-tion as ℎ → 0 for each method. Do they correspond to our analytical


expectations?

Even Runge–Kutta methods may not be good enough without adaptivity: consider the ODE

̇ ( ) =exp [ − sin( )] .

Integrate it using RK4 from = 0 to = 5 with a step size ℎ = 10−2.

−3

Plot both solutions ( ) as a function of . What do you observe? What do you think is happening?

Exercise 2: Adaptivity in the Euler method

In this exercise we will invetigate adaptivity in ODE solvers by taking the sim-plest case: an adaptive Euler method.

Consider one step of the Euler method. Write down the local (single-step) error in terms of the step size ℎ and the unknown constant . Call the approximation obtained at the end of the step (1).

Now consider taking two consecutive Euler steps of size /2. Would you expect this to give a better or a worse approximation to the true solution? Write down the total error after taking the two steps, assuming that the constant is the same for both. Call the approximation at the end of this combined step (2).

Define Δ as the difference between the two approximations. Use this

to find the step size ℎ′ that will give an error per unit time of a given size

.

Use this derivation to write an adaptive Euler integrator adaptive_euler(f, t0, t_final, epsilon) that tries to keep the global error less than , using an update rule similar to the one we discussed in class. Add a multiplica-tive factor 0.9 to that rule to make the method behave better.

Use it to integrate the same ODE as in exercise 1. Plot the step size taken as a function of time.

Now integrate the equation for the van der Pol oscillator:

2

as a = 5

( ,

̈ − (1 − ) ̇ + = 0,

( )

̇ )

= 0

and

̇ = 1

.

with

. Use initial conditions

7. Plot trajectories in

phase

space and (separately) the solution

0

0

function of .


Plot the step size as a function of time. What do you observe? How do you interpret this?

Exercise 3: SIR model In this exercise we will study the SIR model of the dynamics of an infectious disease outbreak (“epidemic”) in a population.

1. Use e.g. RK4 to solve the SIR equations:

= −

(1)

=−

(2)

̇

̇=

(3)

̇

Here is the proportion of the population which is infectious. is the rate of contact between susceptible and infectious individuals, and the recovery rate.

Use 0 = 0.99 and 0 = 0.01.

2. Make an interactive visualization, varying and in, say, the range 0 to

1.

What do you observe? Can you interpret this?

By summing the equations we see that + + should be constant (equal to the total population, assuming no births or deaths). For repre-sentative parameter values = 0.1 and = 0.05, how well does the numerics conserve this quantity?

3
