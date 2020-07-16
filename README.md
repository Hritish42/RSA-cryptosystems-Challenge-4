# RSA-cryptosystems-Challenge-4
(a) Generate Public and private keys of two communicating parties.

(b) Encrypt a short text message of your choice with their RSA /ElGamal key and send
them the encrypted message (as a number, or as a sequence of numbers if your message
is longer than the block size for their n).

(c) Decrypt the encrypted message you receive from your partner.

## Instructions
Check Pdf for more and detailed solutions.

## Usage

```python
import random
  def M_i(e, phi):
  d = 0
  x1 = 0
  x2 = 1
  y1 = 1
  temporary = phi
  while e > 0:
    t1 = temporary/e
    temp2 = temporary - t1 * e
    temporary = e
    e = temp2
    x = x2- t1* x1
    y = d - t1 * y1
    x2 = x1
    x1 = x
    d = y1
    y1 = y
    if temporary == 1:
    return d + phi
  def caus(k, l):
    while l != 0:
      k, l = l, k % l
    return k
  def is_prime(num):
    if num == 2:
    return True
    if num < 2 or num % 2 == 0:
    return False
  for n in xrange(3, int(num**0.5)+2, 2):
    if num % n == 0:
      return False
    return True
  def gen_pair(p, q):
    if not (is_prime(p) and is_prime(q)):
    raise ValueError('Both numbers must be prime.')
    elif p == q:
    raise ValueError('p and q cannot be equal')
    n = p * q
    phi = (p-1) * (q-1)
    e = random.randrange(1, phi)
    g = caus(e, phi)
    while g != 1:
      e = random.randrange(1, phi)
      g = caus(e, phi)
      d = M_i(e, phi)
      return ((e, n), (d, n))
  def encrypt(pk, plaintext):
    key, n = pk
    cipher = [(ord(char) ** key) % n for char in plaintext]
    return cipher
    def decrypt(pk, ciphertext):
    key, n = pk
    plain = [chr((char ** key) % n) for char in ciphertext]
    return ''.join(plain)
   if __name__ == '__main__':
    p = int(raw_input("Enter 1st prime number (17, 19, 23, ....): "))
    q = int(raw_input("Enter 2nd prime number : "))
    public, private = gen_pair(p, q)
    print "Public key ", public ," Private key ", private
    message = raw_input("Message to encrypt with private key: ")
    encrypted_msg = encrypt(private, message)
    print "Encrypted message : "
    print ''.join(map(lambda x: str(x), encrypted_msg))
    print "Decrypting message with public key ", public ," . . ."
    print "Your message is:"
    print decrypt(public, encrypted_msg)
```

## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.

## License
[MIT](https://choosealicense.com/licenses/mit/)
