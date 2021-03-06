# Finding eigenvalues and eigenvectors
Finding a selection of eigenvalues and corresponding (right) eigenvectors of a linear map can
be accomplished with the `eigsolve` routine:
```@docs
eigsolve
```

For a general matrix, eigenvalues and eigenvectors will always be returned with complex values
for reasons of type stability. However, if the linear map and initial guess are real, most of
the computation is actually performed using real arithmetic, as in fact the first step is to
compute an approximate partial Schur factorization. If one is not interested in the eigenvectors,
one can also just compute this partial Schur factorization using `schursolve`.
```@docs
schursolve
```
Note that, for symmetric or hermitian linear maps, the eigenvalue and Schur factorizaion are
equivalent, and one can only use `eigsolve`.

Another example of a possible use case of `schursolve` is if the linear map is known to have
a unique eigenvalue of, e.g. largest magnitude. Then, if the linear map is real valued, that
largest magnitude eigenvalue and its corresponding eigenvector are also real valued. `eigsolve`
will automatically return complex valued eigenvectors for reasons of type stability. However,
as the first Schur vector will coincide with the first eigenvector, one can instead use
```julia
T, vecs, vals, info = schursolve(A, x⁠₀, 1, :LM, Arnoldi(...))
```
and use `vecs[1]` as the real valued eigenvector (after checking `info.converged`) corresponding
to the largest magnitude eigenvalue of `A`.
