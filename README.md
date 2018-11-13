# AES in GDScript

AES in GDScript (AESIG) implements AES cryptography in GDScript. It consists of only one script file, `AES.gd`. Either load this script in your project's AutoLoad, or attach it to a Node and make it a scene.

## Usage
To encrypt, call the following function:

`encrypt(plaintext, key, iv = null, pad_type = PadType.PKCS7)`

To decrypt, call the following function:

`decrypt(ciphertext, key, iv = null, pad_type = PadType.PKCS7)`

These functions return the ciphertext and decrypttext as PoolByteArrays, respectively.

With the exception of `pad_type`, each of these parameters must be either a PoolByteArray, Array, or string. `iv` may additionally be `null` for ECB. The script will convert these inputs to PoolByteArrays.

For IV/key generation, AESIG includes a helper function to generate random-byte PoolByteArrays:

`rand_bytes(size)`

Note that this function does not reseed the RNG, users will have to call `randomize()` in their own code.

## Features

### Key Sizes
AESIG supports three key sizes: 128-bit, 192-bit, and 256-bit. To specify the key size, pass in a key of the appropriate size and AESIG will detect the key size.

### Modes of Operation
AESIG supports two modes of operation: ECB and CBC. To specify the mode, pass in a 128-bit IV for CBC mode or pass in a null IV for ECB mode.

### Padding
AESIG supports two padding schemes: no padding and PKCS7 padding. An enumeration specifies the padding:

`enum PadType {NONE, PKCS7}`

If no padding is used, ensure the plaintext size is a multiple of 16 bytes.
