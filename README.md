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
