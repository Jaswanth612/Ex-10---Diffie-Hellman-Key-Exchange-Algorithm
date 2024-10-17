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
    printf("Enter Siva private key: ");
    scanf("%d", &a);
    printf("Enter Karthi private key: ");
    scanf("%d", &b);
    
    // Public keys (computed from private keys)
    int A = modExp(g, a, p);  // Alice's public key
    int B = modExp(g, b, p);  // Bob's public key
    
    printf("Siva Public Key: %d\n", A);
    printf("Karthi Public Key: %d\n", B);
    
    // Shared secret keys (computed from the other's public key and own private key)
    int sharedKeySiva = modExp(B, a, p);  // Alice computes the shared secret key
    int sharedKeyKarthi = modExp(A, b, p);    // Bob computes the shared secret key
    
    printf("Shared Secret Key (Siav): %d\n", sharedKeySiva);
    printf("Shared Secret Key (Karthi): %d\n", sharedKeyKarthi);
    
    // The shared keys should be the same
    if (sharedKeySiva == sharedKeyKarthi) {
        printf("Key Exchange Successful! Shared Secret Key: %d\n", sharedKeySiva);
    } else {
        printf("Key Exchange Failed!\n");
    }

    return 0;
}
```
## OUTPUT:

![image](https://github.com/user-attachments/assets/1820c585-9caf-4ad8-bb4f-cbc2fa0d3412)

## RESULT:
The program for the Diffie-Hellman algorithm is executed successfully, and Alice and Bob have securely derived a shared secret key.
