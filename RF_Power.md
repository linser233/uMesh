## TX Power Parameter Notes

![image](https://github.com/linser233/uMesh/blob/main/RF_Power.png)

Based on the measured output curves, the following relationships can be derived:

- **For the 30 dBm SKU**:  
  
 ` Pout ≈ 11.75 + 0.85 * Pset `

- **For the 33 dBm SKU**:  
 
 ` Pout ≈ 21 + 0.55 * Pset `

**Important:**  
The `Pset` parameter must not exceed **22** (`SX126X_MAX_POWER = 22`).  
Setting output power beyond 22 dBm **may cause permanent damage to the module**.
