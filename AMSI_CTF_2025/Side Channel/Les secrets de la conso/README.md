# AMSI CTF 2025 - Side Channel : Les Secrets de la conso

- Write-Up Author:  [Atlas](https://github.com/Atlas002) - [0xECE - CyberSharks](https://ctftime.org/team/389816)

- All credits for the challenge go to [AMSI](https://www.linkedin.com/company/association-du-master-s%C3%A9curit%C3%A9-informatique/)

<details>
<summary>Flag</summary>
AMSI{2b7e151628aed2a6abf7158809cf4f3c}
</details>

## Challenge Description:

La clé se cache dans cette consommation de AES128, bon courage.

Flag format : AMSI{key_hexa}

Exemple : AMSI{f3d9c4ab7610efbb29a3dd5e8e1b29f0}

[traces.p](src/traces.p)

## Write up  



### Challenge Overview

The goal was to recover a 128-bit AES key hidden in a set of power‐consumption traces. We were given:

* **`traces.p`**: a Python pickle file containing:

  * **`traces`**: 50 power‐measurement traces, each with 5 000 sample points.
  * **`plaintexts`**: 50 corresponding 16-byte plaintext blocks.

We know the device encrypts each plaintext under AES-128, and the side‐channel leakage (power consumption) correlates with certain internal byte values. The flag format is `AMSI{key_hexa}`.

---

### 1. Loading and Inspecting the Data

1. **Unpickle** the file in Python:

   ```python
   import pickle
   with open('traces.p', 'rb') as f:
       data = pickle.load(f)
   traces = data['traces']        # shape: (50, 5000)
   plaintexts = data['plaintexts']  # shape: (50, 16)
   ```
2. **Check shapes** to confirm:

   ```python
   len(traces)       # 50
   len(traces[0])    # 5000 samples each
   len(plaintexts)   # 50
   len(plaintexts[0])# 16 bytes each
   ```

---

### 2. Choosing a Leakage Model: Hamming Weight

* **Leakage assumption**: At certain points in time, the device’s instantaneous power draw is roughly proportional to the **Hamming weight** (number of ‘1’ bits) of some intermediate AES byte.
* We target the very first byte of the state **immediately after** the SubBytes step in round 1. Why? It’s a common choice (“first‐byte attack”) and gives a clear statistical signal.

---

### 3. Correlation Power Analysis (CPA)

#### 3.1. Hypothesis for One Key Byte

For a **candidate key byte** $k$ (0–255) and trace index $i$:

1. Compute the intermediate value:

   $$
     v_i(k) \;=\; \text{AES\_SBox}\bigl(\text{plaintexts}[i][0] \oplus k\bigr)
   $$
2. Compute its Hamming weight:

   $$
     h_i(k) \;=\; \text{HW}\bigl(v_i(k)\bigr).
   $$
3. Build a vector $\mathbf{h}(k) = [\,h_i(k)\,]_{i=1\dots50}$.

#### 3.2. Correlating with Real Traces

For each of the 5 000 time samples $t$:

* We have the vector of real measured consumptions $\mathbf{T}_t = [\,\text{traces}[i][t]\,]_{i=1\dots50}$.
* Compute the **Pearson correlation coefficient** between $\mathbf{h}(k)$ and $\mathbf{T}_t$.

Then take the **maximum absolute correlation** over all $t$:

$$
  \rho_{\max}(k) \;=\; \max_{t}\,\bigl|\mathrm{corr}\bigl(\mathbf{h}(k), \mathbf{T}_t\bigr)\bigr|.
$$

#### 3.3. Picking the Best Key Byte

* The correct key byte $k^*$ will yield the **highest** $\rho_{\max}(k)$ among all 256 candidates, because its hypothetical Hamming‐weight pattern best matches the observed leakage.

---

### 4. Repeating for All 16 Bytes

Simply repeat the above process independently for each key‐byte position $j=0,\dots,15$, using `plaintexts[i][j]` each time:

1. Loop over key positions.
2. For each, loop over $k=0\ldots255$ to build $\mathbf{h}(k)$.
3. Compute correlations against the 50 traces across all 5 000 time samples.
4. Select the $k$ with the highest max‐correlation.

You end up with 16 recovered bytes $k_0, k_1, \dots, k_{15}$.

---

### 5. Assembling the Final Key

* Collect the bytes in order:

  ```
  k = [2b, 7e, 15, 16, 28, ae, d2, a6, ab, f7, 15, 88, 09, cf, 4f, 3c]
  ```
* Convert to a continuous hex string:

  ```
  2b7e151628aed2a6abf7158809cf4f3c
  ```
* Format as the CTF flag:

  ```
  AMSI{2b7e151628aed2a6abf7158809cf4f3c}
  ```

---

### 6. Conclusion

By carrying out a standard **Correlation Power Analysis** on the first‐round SubBytes output, using a simple Hamming‐weight leakage model, we extract each key byte reliably. This method leverages statistical correlation rather than brute forcing the entire key at once, making it practical even with modest numbers of traces (50 in our case).


## Results

`AMSI{2b7e151628aed2a6abf7158809cf4f3c}`