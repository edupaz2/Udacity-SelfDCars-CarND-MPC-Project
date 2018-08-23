# CarND-Controls-MPC RUBRIC
Self-Driving Car Engineer Nanodegree Program

---

## Implementation

* The Model: we are using the model presented in the classroom.
  * State: [x, y, v, psi, cte, epsi]
  * Actuators: [delta, a]
  * Update Equations: 
    * x_[t+1] = x[t] + v[t] * cos(psi[t]) * dt
    * y_[t+1] = y[t] + v[t] * sin(psi[t]) * dt
    * psi_[t+1] = psi[t] + v[t] / Lf * delta[t] * dt
    * v_[t+1] = v[t] + a[t] * dt
    * cte[t+1] = f(x[t]) - y[t] + v[t] * sin(epsi[t]) * dt
    * epsi[t+1] = psi[t] - psides[t] + v[t] * delta[t] / Lf * dt
    * where Lf in a constant of the center of mass of the vehicle.

* Timestep and Elapsed Duration (N & dt)
  * N=20
  * dt=0.05
  * The values were chosen to look forward 1 second into the future.
  * Other values tested were:
    * N=10, dt=0.1.
    * N=25, dt=0.05.
* Polynomial Fitting and MPC Preprocessing.
  * Preprocessing of the waypoints: in order to simplify our reference coordinate system, I make the variables (x, y, psi)  be zero. In order to do that I have to change the reference coordinate system to all waypoints (translation and rotation).
  * A 3rd order polynomial is fitted to the 6 waypoints given by using the `function polyfit`.
* Model Predictive Control with Latency
  * There is no extra functionality for dealing with latency besides the provided one: this_thread::sleep_for(chrono::milliseconds(100));
