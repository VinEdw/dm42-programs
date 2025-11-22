# DM42 Programs

This is a collection of programs on my [DM42n](https://www.swissmicros.com/product/model-dm42n) calculator.
The programs should be compatible with [Free42](https://thomasokken.com/free42/).
As of now, I keep them all in one file `PROGRAMS.txt`.

Note: I usually keep my calculator in [`NSTK` mode](https://thomasokken.com/free42/#big-stack).

## Descriptions

### `QUAD`

Solve quadratic equations in the form $Ax^2 + Bx + C = 0$ using the quadratic formula.
Enter the values for the constants, press `R/S` to get the first solution, then press `R/S` again to get the second solution.

$$
x = \frac{-B \pm \sqrt{B^2 - 4AC}}{2A}
$$

### `FX`

A placeholder function that takes one input from the stack and returns one value to the stack.
Edit it to have the desired function of interest.

$$
f(x) = \ldots
$$

### `SUMFX`

Sum the function `FX` from `START` to `STOP`, returning the result and saving it in `SUM`.
The step size is equal to 1.

$$
\mathrm{SUM} = \sum_{n = \mathrm{START}}^{\mathrm{STOP}} f(n)
$$

### `PRDFX`

Take the product of the function `FX` from `START` to `STOP`, returning the result and saving it in `PROD`.
The step size is equal to 1.

$$
\mathrm{PROD} = \prod_{n = \mathrm{START}}^{\mathrm{STOP}} f(n)
$$

### `dFX`

Approximate the derivative of `FX` with respect to `X` at the given input value from the stack, returning the value to the stack.
The derivative is approximated using a symmetric difference quotient with a small step size ($h = 1 \times 10^{-6}$).

$$
f'(x) = \lim_{h \to 0} \frac{f(x + h) - f(x - h)}{2h}
$$

### `GX`

A placeholder function that takes one input, `X`, from a variable menu, and returns one value to the stack.
Edit it to have the desired function of interest.

$$
g(x) = \ldots
$$

### `PRIME`

Append on the stack the lowest, positive, non-one factor of the input integer on the stack.

### `GCF`

Take the two input integers on the stack and return their greatest common factor.

### `XGCF`

Use the extended Euclidean algorithm to solve the following equation for the given inputs $a$ and $b$.

$$
a x + b y = \mathrm{gcf}(a,b)
$$

Note that $x$ and $y$ are integers.
Return $\mathrm{gcf}(a,b)$, $x$, and $y$.

### `LCM`

Take the two input integers on the stack and return their lowest common multiple.

### `IDMAT`

Create an identity matrix with the dimension given on the stack, and return the new matrix to the stack.

$$
I_n = \begin{bmatrix}
  1 & 0 & 0 & \dots & 0 \\
  0 & 1 & 0 & \dots & 0 \\
  0 & 0 & 1 & \dots & 0 \\
  \vdots & \vdots & \vdots & \ddots & \vdots \\
  0 & 0 & 0 & \dots & 1
\end{bmatrix}
$$

### `RREF`

Take the input matrix on the stack and put it into reduced row echelon form (RREF), returning the new matrix on the stack.

### `MPWR`

Take the input matrix and the given integer power on the stack, and return the matrix raised to that power.

$$
\mathrm{MPWR}(A, p) = A^p
$$

### `MEXP`

Approximate the matrix exponential of the input matrix.
The Taylor Series for $e^M$ is as follows.

$$ \exp(M) = \sum\limits_{n=0}^{\infty} \frac {M^n} {n!} $$

The amount to bump the result on each iteration is $B_n$.

$$ B_n = \frac{M^n}{n!} $$

$B_n$ can be recursively calculated as follows.

$$ B_{n+1} = \frac{1}{n+1} B_n M $$
$$ B_0 = I $$

Iterations continue until the Frobenius norm (`FNRM`) of $B_n$ falls below some `err` threshold.
For this program, `err` was set to $10^{-9}$.

$$ \mathrm{FNRM}(B) < \mathrm{err} $$

The Frobenius norm of a matrix $A$ is calculated as follows.

$$ \mathrm{FNRM}(A) = \sqrt{ \sum\limits_{i} \sum\limits_{j} |a_{ij}|^2 } = \sqrt{ \mathrm{Tr}(A A^\dagger) } $$

Notice that $\mathrm{FNRM}(A) \ge a_{ij}$.
Thus, by ensuring $\mathrm{FNRM}(B_n) < \mathrm{err}$, that ensures every element of $B_n$ is less than `err`.

### `MMOD`

Take the input matrix and the given modulus on the stack, and perform the `MOD` operation on each element of the matrix.
Return the new matrix.

### `MINOR`

Remove from the input matrix the specified row and column, returning the minor matrix.

### `mDET`

Take the determinant of the minor matrix for the input matrix at the specified row and column.

### `COFACT`

Return the cofactor of the input matrix at the specified row and column.
This is calculated by taking the minor determinant, then potentially flipping the sign according to the position in the matrix.

$$
\begin{bmatrix}
  (+) & (-) & (+) & \dots \\
  (-) & (+) & (-) & \dots \\
  (+) & (-) & (+) & \dots \\
  \vdots & \vdots & \vdots & \ddots \\
\end{bmatrix}
$$

### `ADJ`

Calculate the adjugate of the input matrix.
The adjugate matrix is the transpose of the matrix of the cofactors of the input matrix.

$$
A \mathrm{adj}(A) = \mathrm{det}(A) \cdot I
$$

### `Tr`

Calculate the trace of the input square matrix by summing the elements on its main diagonal.

### `CHPLY`

Calculate the characteristic polynomial of the input square matrix using the Faddeev-LeVerrier algorithm.

$$
p_A(t) = \det(tI - A) = \sum_{n=0}^{N} c_n t^n
$$
$$
c_N = 1
$$
$$
c_{N-m} = -\frac{1}{m} \sum_{k=1}^{m} c_{N-m+k} \mathrm{Tr}[A^k]
$$

### `LENGTH`

Program for length unit conversions.
Enter the starting value, select the starting units, then select the desired units.

### `SPEED`

Program for speed unit conversions.
Enter the starting value, select the starting units, then select the desired units.

### `TEMP`

Program for temperature unit conversions.
Enter the starting value, select the starting units, then select the desired units.

### `MASS`

Program for mass unit conversions.
Enter the starting value, select the starting units, then select the desired units.

### `ENERGY`

Program for energy unit conversions.
Enter the starting value, select the starting units, then select the desired units.

### `PRESS`

Program for pressure unit conversions.
Enter the starting value, select the starting units, then select the desired units.

### `HYPER`

Program to create a custom menu containing the hyperbolic trig functions.

### `FRAC`

Take the input number on the stack and show the fraction approximation (within a tolerance of $1 \times 10^{-9}$).
This approximation is created by traversing the left subtree of the Stern-Brocot tree.
The bounds for the fraction start at $\frac 0 1$ and $\frac 1 1$.
A middle fraction is created by taking the mediant of the lower and higher bounds.
If the input number is lower than the middle fraction, then the middle fraction becomes the new higher bound.
If the input number is greater than the middle fraction, then the middle fraction becomes the new lower bound.
This process repeats until the middle fraction is within tolerance of the input number.

$$
\mathrm{mediant}\left( \frac a b, \frac c d \right) = \frac {a + c} {b + d}
$$

### `Const`

Program to create a custom menu containing various physics constants.
Values were taken from a [page by NIST](https://physics.nist.gov/cuu/Constants/index.html).

### `GetDisp`

Return an integer that holds the flags representing the display format.
This can be helpful for saving the display format.
The display format can then be changed temporarily, perhaps to use the `RND` function, then switched back using `SetDisp`.

### `SetDisp`

Use an integer that holds the flags representing the display format, such as the output of `GetDisp`, to set the display format.

### `LOUD`

Program to create a custom menu with functions to switch between sound intensity level ($\beta$) in dB and sound intensity ($I$) in $\mathrm{W/m^2}$.
Note: $I_0 = 1 \times 10^{-12}~\mathrm{W/m^2}$ is the threshold of (human) hearing.

$$
\beta = (10~\mathrm{dB}) \log\left( \frac {I} {I_0} \right)
$$

$$
I = I_0 \cdot 10^{\beta / (10~\mathrm{dB})}
$$

### `DOPLR`

Program for the built-in `SOLVER` that implements the Doppler effect equation.
- $v_L > 0$ when the listener moves toward the source
- $v_S > 0$ when the source moves away from the listener

$$
f_L = \frac {c + v_L} {c + v_S} f_S
$$

### `STDGW`

Program for the built-in `SOLVER` that implements the standing wave equation for a transverse wave in a string.

- $v = f \lambda$
- $\lambda = \frac{2L}{n}$
- $v = \sqrt\frac{F_T}{\mu}$

### `GASLW`

Program for the built-in `SOLVER` that implements the ideal gas law.

$$
PV = nRT
$$

### `GREET`

Have the calculator say a friendly greeting to your friends.

### `COUNTER`

A tally counter program.
The up arrow increases the `CNT` by the `INC`.
The down arrow decreases the `CNT` by the `INC`.
`CNT` and `INC` can be viewed, recalled, or updated using the `SET` variable menu.
Exit the `SET` menu by pressing the `R/S` button.

### `RNG`

Take the maximum and minimum integer values from the stack, and return a random integer between them.

### `POLYX`

Evaluate the polynomial array in the Y-register at the x-value in the X-register.
Return the polynomial in the Y-register for chaining, and the result in the X-register.

### `POLYn`

Create a polynomial array of the input degree.
Each coefficient should be 0, except the coefficient for the highest degree term which should be 1.

$$
n \rightarrow x^n
$$

### `POLYr`

Reduce the size of the input polynomial array by removing any 0 coefficients for the highest degree terms, returning the reduced polynomial array.

### `POLY+`

Add the two input polynomial arrays and return the resulting polynomial array.

### `POLY×`

Multiply the two input polynomial arrays and return the resulting polynomial array.

### `POLY÷`

Divide the polynomial array in the Y-register $P_1(x)$ by the polynomial array in the X-register $P_2(x)$, returning polynomial arrays for the quotient $Q(x)$ and the remainder $R(x)$.

$$
\frac {P_1(x)} {P_2(x)} = Q(x) + \frac {R(x)} {P_2(x)}
$$

### `POLYs`

Program for the built-in `SOLVER` that finds the roots of polynomial matrix stored in `POLY`.
The roots are stored in `X`

### `PFD`

Perform partial fraction decomposition.
The numerator polynomial $p(x)$ should have a lower degree than the denominator polynomial $q(x)$.
The Y-register should hold the polynomial array for $p(x)$.

The X-register should hold an array with 4 columns and rows representing the linear factors and irreducible quadratic factors of $q(x)$.
Each row represents a linear/quadratic factor.
Column 1 holds the coefficient for the constant term.
Column 2 holds the coefficient for the linear term.
Column 3 holds the coefficient for the quadratic term.
Column 4 holds an integer for how many times the factor repeats.

$$
q(x) = (a_0 + a_1 x)^n (b_0 + b_1 x + b_2 x^2)^k \ldots
$$
$$
\begin{align*}
  \frac {p(x)} {q(x)} =& \frac {A_1} {(a_0 + a_1 x)} + \frac {A_2} {(a_0 + a_1 x)^2} + \ldots + \frac {A_k} {(a_0 + a_1 x)^k} \\
  &+ \frac {B_1 x + C_1} {(b_0 + b_1 x + b_2 x^2)} + \frac {B_2 x + C_2} {(b_0 + b_1 x + b_2 x^2)^2} + \ldots + \frac {B_n x + C_n} {(b_0 + b_1 x + b_2 x^2)^n} \\
  &+ \ldots
\end{align*}
$$

### `RCS`

Program to create a custom menu with functions to switch between rectangular, cylindrical, and spherical coordinates.
It also contains shortcuts to `ST→[]` and `[]→ST`.

- Rectangular → Cylindrical
    - $r = \sqrt{x^2 + y^2}$
    - $\phi = \mathrm{atan2}(y, x)$
    - $z = z$
- Cylindrical → Rectangular
    - $x = r \cos(\phi)$
    - $y = r \sin(\phi)$
    - $z = z$
- Rectangular → Spherical
    - $r = \sqrt{x^2 + y^2 + z^2}$
    - $\theta = \arccos( \frac z r )$
    - $\phi = \mathrm{atan2}(y, x)$
- Spherical → Rectangular
    - $x = r \sin(\theta) \cos(\phi)$
    - $y = r \sin(\theta) \sin(\phi)$
    - $z = r \cos(\theta)$

### `ST→[]`

Combine the coordinate is the X-, Y-, and Z-registers into a 1×3 matrix in the X-register.

### `[]→ST`

Return the coordinates in a 1×3 matrix to the X-, Y-, and Z-registers.

### `CONJ`

Return the complex conjugate of the input in the X-register.

$$
z = a + b i
$$

$$
z^* = a - b i
$$

### `CCSTM`

Program to clear the second and third rows of the custom menu.
When paired with other programs that modify those rows of the custom menu, it provides a way to switch between sets of functions.
This allows functions more relevant to the problem at hand to be made readily available.
The first row of the custom menu is reserved for functions that should always be easily accessed.

### `PTOOLS`

Program to edit the custom menu to contain programming tools on the second row.
These are functions often needed when writing programs.

### `DEBUG`

Program to edit the custom menu to contain debugging tools on the second row.
These are functions often needed when debugging programs.

### `UNITS`

Program to edit the custom menu to contain unit conversion programs on the second row.

### `T/D`

Program to edit the custom menu to contain time and date functions on the second and third rows.

### `POLY`

Program to edit the custom menu to contain polynomial related functions.
Polynomials are represented using single row arrays where each element holds a coefficient for a different term.
The first element holds the coefficient for $x^0$, the second element holds the coefficient for $x^1$, the third element holds the coefficient for $x^2$, and so on.

$$
p_n(x) = C_0 + C_1 x + C_2 x^2 + \ldots + C_n x^n
$$
$$
p_n(x) \rightarrow \begin{bmatrix}
  C_0 & C_1 & C_2 & \ldots & C_n
\end{bmatrix}
$$

### `VEC`

Program to edit the custom menu to contain vector related functions on the second and third rows.

### `MTRX`

Program to edit the custom menu to contain matrix related functions on the second and third rows.
