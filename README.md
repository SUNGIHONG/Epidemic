# Epidemic
Epidemics paper materials

## How to use the code (for different cities)

When applying the code to a different city, please update the following sections:

1. **Section 0 (Load Data)**  
   Replace the dataset with the corresponding data for the target city.

2. **Section 5 (Training Window)**  
   Modify `train_start` and `T_train` (training window length).  
   You can experiment with multiple training windows for the same city.  
   In this paper, we use `T_train = 90, 120, 150`.

3. **Population Size**  
   Update the population parameter `N_pop` for the selected city.

4. **Disease Parameters**  
   Adjust disease-related parameters (e.g., transmission and progression rates) as appropriate for the city.

5. **Seasonal Peak Date**  
   Modify the seasonal peak timing (`t0`) based on the region.

6. **Mandate Data**  
   Update the mandate periods and levels to reflect the policies of the selected city/state.

## ODE Integration and Daily Data Alignment

The model is formulated as a continuous-time ODE system. In the code, the ODE is solved using `scipy.integrate.solve_ivp`.

```python
sol = solve_ivp(
    ode_wrapper,
    t_span,
    y0,
    method=method,      # default: "RK45"; can also use "Radau"
    t_eval=time,        # daily observation times
    rtol=1e-6,
    atol=1e-9
)
```

Here, method="RK45" uses an adaptive Runge–Kutta solver. The solver internally chooses its own time steps for numerical accuracy. These internal steps do not correspond to days. Daily alignment is handled through t_eval=time. For example, when
```python
time = np.arange(0, T_train)
```
the model output is evaluated at
```python
t = 0, 1, 2, ..., T_train-1
```
which corresponds to daily observation times in the dataset.

Thus, a training window such as T_train = 90 means that the continuous-time ODE is solved over a 90-day horizon, and the resulting trajectory is sampled at daily timestamps for comparison with the data. It does not mean that the solver takes exactly 90 internal steps.
