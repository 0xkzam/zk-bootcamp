# zkSNARK theory / PLONK

## Polynomial Introduction
**Look into properties of polynomials and interpolation.

## Polynomial Commitment Schemes (PCS)

A polynomial commitment is a cryptographic derivation of a polynomial (a short object) that doesn't reveal the coefficients or any specific values of the original polynomial. 

#### Properties of a commitment
- Binding: Once a commitment is made it cannot be changed. The prover is bound to it and cannot later claim a commitment that refers to a different polynomial.
- Hiding: The commitment doesn't reveal anything about the committed data until the prover chooses to reveal them.

#### Commitment function families
1. Polynomial commitments
   - Committed using a univariate polynomial (ie. a polynomial that involves only one variable)
   - E.g., $P(x)=a_nx^n+a_{n-1}x^{n-1}+...+a_1x+a_0$
   - NOTE: PCS generally refers to this univariate polynomial family. 
  
2. Multi-linear commitments
   - Committed using a multilinear polynomial (ie. a polynomial of degree at most one)
   - E.g., $P(x,y,z)=x+y+z+xy+xz+yz+xyz+2$ 

3. Linear commitments
   - If you commit to a value x using a commitment function C, and to another value y similarly, you can perform linear operations on these commitments (such as addition or scalar multiplication)
   - E.g., $C(ax+by)=aC(x)+bC(y)$

#### KZG PCS

## Proving Systems in general

## zkSNARK process


## Plonkish protocols