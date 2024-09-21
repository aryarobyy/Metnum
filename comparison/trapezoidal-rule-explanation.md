# Penjelasan Implementasi Modified Trapezoidal Rule

Mari kita bandingkan rumus dari jurnal dengan implementasi kode Python:

## Rumus dari Jurnal (Teorema 3.1)

```
I^α_a f(x) ≈ (h^(1-α) / (2Γ(α+1))) * Σ_{k=1}^n [(kh)^α - ((k-1)h)^α] * [f(x_k) + f(x_{k-1})]
```

di mana:
- α adalah orde fraksional
- h adalah lebar subinterval ((b-a)/n)
- Γ adalah fungsi gamma
- n adalah jumlah subinterval
- x_k adalah titik evaluasi ke-k

## Implementasi Python

```python
def modified_trapezoidal_rule(f, a, b, alpha, n):
    h = (b - a) / n
    x = np.linspace(a, b, n+1)
    y = f(x)
    
    integral = 0
    for k in range(1, n+1):
        integral += ((k*h)**alpha - ((k-1)*h)**alpha) * (y[k] + y[k-1])
    
    integral *= (h**(1-alpha)) / (2 * gamma(alpha+1))
    return integral
```

## Penjelasan Kesesuaian

1. **Perhitungan h**: 
   ```python
   h = (b - a) / n
   ```
   Ini sesuai dengan definisi h dalam rumus.

2. **Pembuatan array x dan y**:
   ```python
   x = np.linspace(a, b, n+1)
   y = f(x)
   ```
   Ini membuat array titik evaluasi x_k dan nilai fungsi f(x_k).

3. **Loop utama**:
   ```python
   for k in range(1, n+1):
       integral += ((k*h)**alpha - ((k-1)*h)**alpha) * (y[k] + y[k-1])
   ```
   Ini mengimplementasikan penjumlahan (Σ) dalam rumus. Perhatikan bahwa:
   - `(k*h)**alpha - ((k-1)*h)**alpha` sesuai dengan `[(kh)^α - ((k-1)h)^α]`
   - `y[k] + y[k-1]` sesuai dengan `[f(x_k) + f(x_{k-1})]`

4. **Faktor pengali akhir**:
   ```python
   integral *= (h**(1-alpha)) / (2 * gamma(alpha+1))
   ```
   Ini sesuai dengan faktor `(h^(1-α) / (2Γ(α+1)))` dalam rumus.

Dengan demikian, kita dapat melihat bahwa implementasi Python secara tepat mengikuti rumus yang diberikan dalam jurnal. Perbedaan utamanya hanya dalam notasi dan penggunaan struktur data Python (seperti array NumPy) untuk efisiensi komputasi.
