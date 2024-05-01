# Information Security (IS)

### Practical 1
```python
text = "Helloworld"

for ch in text:
    print(ch + " & 127 : " + chr(ord(ch) & 127), end="\t\t")
    print(ch + " | 127 : " + chr(ord(ch) | 127), end="\t\t")
    print(ch + " ^ 127 : " + chr(ord(ch) ^ 127), end="\n")
```

### Practical 2
```python
import math

def encrypt(plaintext, key):
    ciphertext = [''] * key
    for col in range(key):
        pointer = col
        while pointer < len(plaintext):
            ciphertext[col] += plaintext[pointer]
            pointer += key
            print(ciphertext)
    return ''.join(ciphertext)

def decrypt(encrypted_text, key):
    num_of_rows = key
    num_of_cols = math.ceil(len(encrypted_text) / key)
    num_of_shaded_boxes = (num_of_rows * num_of_cols) - len(encrypted_text)

    plaintext = [''] * num_of_cols

    col = 0
    row = 0

    for symbol in encrypted_text:
        plaintext[col] += symbol
        col += 1
        if (col == num_of_cols) or (col == num_of_cols - 1 and row >= num_of_rows - num_of_shaded_boxes):
            col = 0
            row += 1
            print(plaintext)
    return ''.join(plaintext)

plaintext = "transposition technique using python"
key = 8

encrypted_text = encrypt(plaintext, key)
print("Encrypted text:", encrypted_text)

decrypted_text = decrypt(encrypted_text, key)
print("Decrypted text:", decrypted_text)
```

### Practical 3
```python
from Crypto.Cipher import DES
from Crypto.Random import get_random_bytes
from Crypto.Util.Padding import pad, unpad

def encrypt_des(plaintext, key):
    cipher = DES.new(key, DES.MODE_ECB)
    padded_plaintext = pad(plaintext.encode(), DES.block_size)
    ciphertext = cipher.encrypt(padded_plaintext)
    return ciphertext

def decrypt_des(ciphertext, key):
    cipher = DES.new(key, DES.MODE_ECB)
    decrypted = cipher.decrypt(ciphertext)
    plaintext = unpad(decrypted, DES.block_size)
    return plaintext.decode()

plaintext = "Hello, World!"
key = get_random_bytes(8)

encrypted_text = encrypt_des(plaintext, key)
print("Encrypted text:", encrypted_text.hex())

decrypted_text = decrypt_des(encrypted_text, key)
print("Decrypted text:", decrypted_text)
```
### Practical 4
```python
from Crypto.Cipher import AES
from Crypto.Random import get_random_bytes

def encrypt_aes(plaintext, key):
    cipher = AES.new(key, AES.MODE_EAX)
    ciphertext, tag = cipher.encrypt_and_digest(plaintext.encode())
    return ciphertext, tag, cipher.nonce

def decrypt_aes(ciphertext, tag, nonce, key):
    cipher = AES.new(key, AES.MODE_EAX, nonce=nonce)
    plaintext = cipher.decrypt_and_verify(ciphertext, tag)
    return plaintext.decode()

plaintext = "Hello, World!"
key = get_random_bytes(16)

encrypted_text, tag, nonce = encrypt_aes(plaintext, key)
print("Encrypted text:", encrypted_text.hex())

decrypted_text = decrypt_aes(encrypted_text, tag, nonce, key)
print("Decrypted text:", decrypted_text)
```

### Practical 5
```python
import math

def gcd(a, b):
    temp = 0
    while (1):
        temp = a % b
        if (temp == 0):
            return b
        a = b
        b = temp

p = 3
q = 7
n = p * q
e = 2
phi = (p - 1) * (q - 1)

while (e < phi):
    if (gcd(e, phi) == 1):
        break
    else:
        e = e + 1

k = 2
d = (1 + (k * phi)) / e

msg = 12.0

print("Message data = ", msg)

# Encryption
c = pow(msg, e)
c = math.fmod(c, n)
print("Encrypted data = ", c)

# Decryption
m = pow(c, d)
m = math.fmod(m, n)
print("Original Message Sent = ", m)
```

### Practical 6
```java
import java.util.*;

class DiffieHellmanAlgorithm {

     private static long calculatePower(long x, long y, long P)
    {
        long result = 0;
        if (y == 1){
            return x;
        }
        else{
            result = ((long)Math.pow(x, y)) % P;
            return result;
        }
    }

    public static void main(String[] args)
    {
        long P, G, x, a, y, b, ka, kb;

        Scanner sc = new Scanner(System.in);
        System.out.println("Both the users should be agreed upon the public keys G and P");

        System.out.println("Enter value for public key G:");
        G = sc.nextLong();
        System.out.println("Enter value for public key P:");
        P = sc.nextLong();

        System.out.println("Enter value for private key a selected by user1:");
        a = sc.nextLong();
        System.out.println("Enter value for private key b selected by user2:");
        b = sc.nextLong();

        x = calculatePower(G, a, P);
        y = calculatePower(G, b, P);

        ka = calculatePower(y, a, P);

        kb = calculatePower(x, b, P);

        System.out.println("Secret key for User1 is:" + ka);
        System.out.println("Secret key for User2 is:" + kb);
    }
}
```
