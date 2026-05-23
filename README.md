# EX-NO-11-ELLIPTIC-CURVE-CRYPTOGRAPHY-ECC

## Aim:
To Implement ELLIPTIC CURVE CRYPTOGRAPHY(ECC)

NAME:AVANTHIKA.M


REG NO: 212224110009


## ALGORITHM:

1. Elliptic Curve Cryptography (ECC) is a public-key cryptography technique based on the algebraic structure of elliptic curves over finite fields.

2. Initialization:
   - Select an elliptic curve equation \( y^2 = x^3 + ax + b \) with parameters \( a \) and \( b \), along with a large prime \( p \) (defining the finite field).
   - Choose a base point \( G \) on the curve, which will be used for generating public keys.

3. Key Generation:
   - Each party selects a private key \( d \) (a random integer).
   - Calculate the public key as \( Q = d \times G \) (using elliptic curve point multiplication).

4. Encryption and Decryption:
   - Encryption: The sender uses the recipient’s public key and the base point \( G \) to encode the message.
   - Decryption: The recipient uses their private key to decode the message and retrieve the original plaintext.

5. Security: ECC’s security relies on the Elliptic Curve Discrete Logarithm Problem (ECDLP), making it highly secure with shorter key lengths compared to traditional methods like RSA.

## Program:
```
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y

def inverse(a, p):
    for i in range(1, p):
        if (a * i) % p == 1:
            return i

def add(P, Q, a, p):

    if P.x == Q.x and P.y == Q.y:
        l = ((3 * P.x * P.x + a) * inverse(2 * P.y, p)) % p
    else:
        l = ((Q.y - P.y) * inverse(Q.x - P.x, p)) % p

    x = (l * l - P.x - Q.x) % p
    y = (l * (P.x - x) - P.y) % p

    return Point(x, y)

def multiply(P, k, a, p):
    R = P
    for i in range(k - 1):
        R = add(R, P, a, p)
    return R


print("ECC Key Exchange")

p = int(input("Enter prime number: "))
a = int(input("Enter value of a: "))

gx = int(input("Enter Gx: "))
gy = int(input("Enter Gy: "))

A = int(input("Enter AVANTHIKA private key: "))
B = int(input("Enter M private key: "))

G = Point(gx, gy)

pubA = multiply(G, A, a, p)
pubB = multiply(G, B, a, p)

secret1 = multiply(pubB, A, a, p)
secret2 = multiply(pubA, B, a, p)

print("Shared Secret by AVANTHIKA:", secret1.x, secret1.y)
print("Shared Secret by M:", secret2.x, secret2.y)
```


## Output:
<img width="1087" height="723" alt="Screenshot 2026-05-23 214740" src="https://github.com/user-attachments/assets/de91fbf1-7aac-4d00-9e5c-231c93df29d0" />



## Result:
The program is executed successfully

