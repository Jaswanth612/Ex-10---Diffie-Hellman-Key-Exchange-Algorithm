# Ex-10-Diffie-Hellman-Key-Exchange-Algorithm
## AIM:
To implement the Diffie-Hellman algorithm to securely exchange keys and generate a shared secret key.

## DESIGN STEPS:
Step 1: Design the Diffie-Hellman key exchange algorithm.

Step 2: Implement the algorithm using C.

Step 3: The Diffie-Hellman algorithm uses a large prime number p and a primitive root g. Both Alice and Bob select private keys and exchange public keys computed using the formula:

Public Key = (g^Private Key) % p After exchanging public keys, both compute a shared secret key using:

Shared Secret = (Other's Public Key^Private Key) % p

## PROGRAM:
```
#include <stdio.h>
#include <math.h>

// Function to calculate (base^exp) % mod using modular exponentiation
int modExp(int base, int exp, int mod) {
    int result = 1;
    base = base % mod;
    while (exp > 0) {
        if (exp % 2 == 1) {
            result = (result * base) % mod;
        }
        exp = exp >> 1;
        base = (base * base) % mod;
    }
    return result;
}

int main() {
    // Publicly known values
    int p;  // A large prime number
    int g;   // A primitive root modulo p
    printf("Enter a prime number (p): ");
    scanf("%d", &p);
    printf("Enter a base (g): ");
    scanf("%d", &g);
    
    // Private keys (chosen secretly by Alice and Bob)
    int a, b;
    printf("Enter JAS private key: ");
    scanf("%d", &a);
    printf("Enter JASS private key: ");
    scanf("%d", &b);
    
    // Public keys (computed from private keys)
    int A = modExp(g, a, p);  // Alice's public key
    int B = modExp(g, b, p);  // Bob's public key
    
    printf("JAS Public Key: %d\n", A);
    printf("JASS Public Key: %d\n", B);
    
    // Shared secret keys (computed from the other's public key and own private key)
    int sharedKeyjas = modExp(B, a, p);  // Alice computes the shared secret key
    int sharedKeyjass = modExp(A, b, p);    // Bob computes the shared secret key
    
    printf("Shared Secret Key (JAS): %d\n", sharedKeyjas);
    printf("Shared Secret Key (JASS): %d\n", sharedKeyjass);
    
    // The shared keys should be the same
    if (sharedKeyjas == sharedKeyjass) {
        printf("Key Exchange Successful! Shared Secret Key: %d\n", sharedKeyjas);
    } else {
        printf("Key Exchange Failed!\n");
    }

    return 0;
}
```
## OUTPUT:

![Screenshot 2024-10-17 092205](https://github.com/user-attachments/assets/484a0dfd-3b89-4515-9ea5-9f434855d082)


## RESULT:
The program for the Diffie-Hellman algorithm is executed successfully, and Alice and Bob have securely derived a shared secret key.
