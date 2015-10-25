# ToolBox
Collection of useful tools and tricks for competitive programming

##Modular Exponentiation

```c++
int modPow(long long b, long long e, int m) {
    long long res = 1;
    for (; e; e >>= 1, b = b*b%m) if (e & 1) res = res*b%m;
    return res;
}
````

##Modular Multiplicative Inverse


```c++
void extEuclid(int a, int b, int &x, int &y, int &gcd) {
    x = 0; y = 1; gcd = b;
    int m, n, q, r;
      for (int u=1, v=0; a != 0; gcd=a, a=r) {
          q = gcd / a; r = gcd % a;
          m = x-u*q; n = y-v*q;
          x=u; y=v; u=m; v=n;
      }
}

    // The result could be negative, if it's required to be positive, then add "m"
int modInv(int n, int m) {
    int x, y, gcd;
    extEuclid(n, m, x, y, gcd);
    if (gcd == 1) return x % m;
    return 0;
}

```

###Example
```
Answer = SumDiv( 36^30 ) % MOD                      // Where MOD = 1,000,000,007

A = SumDiv( (2^2 * 3^2) ^ 30 ) % MOD                // Prime factorization of 36
A = SumDiv( 2^60 * 3^60 ) % MOD                     // Exponent rule
A = ( (2^61 - 1) / 1 ) * ( (3^61 - 1) / 2 ) % MOD   // Sum of divisors

// At this point, using modular arithmetic brings us to the answer

A = ( ( (2^61 - 1) / 1 ) % MOD ) *  ( ( (3^61 - 1) / 2 ) % MOD ) % MOD

A =   ( (2^61 - 1) % MOD ) * ( 1^-1 ) % MOD
    * ( (3^61 - 1) % MOD ) * ( 2^-1 ) % MOD
    % MOD
    
// Where x^-1 is the MMI of x, modulo MOD

A =   ( ( modPow(2, 61, MOD) - 1 ) % MOD * modInv(1, MOD) ) % MOD
    * ( ( modPow(3, 61, MOD) - 1 ) % MOD * modInv(2, MOD) ) % MOD
    % MOD
```
