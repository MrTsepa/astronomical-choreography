# Astronomical choreography

## What is this project about

Suppose that we have system of N astronomical objects, who is moved by gravity forces.
Generally this problem is called [N-body problem](https://en.wikipedia.org/wiki/N-body_problem) and its well known that starting from N=3, N-body problem can be solved only for special cases.

This work is covering more narrow situation called [N-body choreography](https://en.wikipedia.org/wiki/N-body_choreography) in which we are looking only for periodic solutions. So our question is: Which periodic orbits are possible for given N? I once discovered Moore's article and was amazed by how elegantly this problem can be solved with variational principle so I decided to implement it and visualize process of numerical learning. Further I will first briefly cover underlying theory and show animated results I achieved.

## Origins

This work is an implemetation of method, proposed in article "Braids in classical gravity" by Cristopher Moore, 1993. This project was prepared during my studying at Skoltech University at Moscow as final project for course "Scientific computing".

## Theory

### What is variational principle

I will start from afar and describe what matematicians call a variational principle. There is a well-known task of finding extremas of a function. Generally speaking this task is to find such <img src="https://render.githubusercontent.com/render/math?math=x"/> that <img src="https://render.githubusercontent.com/render/math?math=y=f(x)"/> is an extremum. Here is quite similiar task: instead of <img src="https://render.githubusercontent.com/render/math?math=x"/> we will have functions and instead of regular function <img src="https://render.githubusercontent.com/render/math?math=f(x)"/> we will have "second-order" function <img src="https://render.githubusercontent.com/render/math?math=F(g)"/> that takes some function (just consider it as curve on coordinate plane) as an input and calculates one number as an output. Here comes variational task: find such curve <img src="https://render.githubusercontent.com/render/math?math=g"/> where <img src="https://render.githubusercontent.com/render/math?math=F(g)"/> will be minimal. I will not cover how this problem can be solved, just check out this [wikipedia page](https://en.wikipedia.org/wiki/Euler%E2%80%93Lagrange_equation).

### How it is connected to physics

It was discovered that mechanical laws (e.g. Newtown laws) can be derived from variational principle. It turns out, that trajectory of a moving body **is** such a minimal curve in case we define <img src="https://render.githubusercontent.com/render/math?math=F(g)"/> as a special concept called *action*. Action <img src="https://render.githubusercontent.com/render/math?math=S"/> is an integral over whole body path of another concept called *Lagrangian* <img src="https://render.githubusercontent.com/render/math?math=\mathcal{L}"/>, which is actually just kinetic energy minus potential energy. Let's look on formulas:

<img src="https://render.githubusercontent.com/render/math?math=S(g)=\int_{t1}^{t2}\mathcal{L}(g(t))dt=\int_{t1}^{t2}(K(g(t))-U(g(t)))dt,"/>

<img src="https://render.githubusercontent.com/render/math?math=g_{real}=\min_{S}g."/>

That's it. All you need to do is find such curve <img src="https://render.githubusercontent.com/render/math?math=g"/> where action <img src="https://render.githubusercontent.com/render/math?math=S"/> is minimal and it will be a real path. That is called the [Principle of least action](https://en.wikipedia.org/wiki/Principle_of_least_action).

### What we do in this work

The principle of least action is used to solve our problem. We start from some approximate trajectories and then comupute <img src="https://render.githubusercontent.com/render/math?math=\frac{dS}{dg}"/> to make gradient descent step and finally find appropriate trajectory.

For complete formulas see following literature:
- "Braids in classical gravity" by Cristopher Moore, 1993
- "New Orbits for the n-Body Problem" by Robert J. Vanderbei

## Results

Let's see what we have

Further for each case there will be three images:
1. starting orbits
2. process of learning, on plot you can see two types of lines:
    - **solid lines** are for optimized trajectories, so for most part of the time they don't represent real gravitational moving
    - **dot lines** are real trajectories from given starting conditions (calculated with leapfrog method)
    
    that mean that we can consider our solution valid when this two types of lines overlap with each other
  
3. resulting orbits and bodies moving along them

For example see the simpliest case of 2 bodies

### Simple 2-body solution

![](images/2-bodies_start.gif)
![](images/2-bodies_evolution.gif)
![](images/2-bodies.gif)

### 3-body oval solution

![](images/3-bodies-oval_evolution.gif)
![](images/3-bodies-oval.gif)

### 3-body eight solution

![](images/3-bodies-eight_evolution.gif)
![](images/3-bodies-eight.gif)

