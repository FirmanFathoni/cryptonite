# cryptonite

**cryptonite** is a lightweight python module that I built for solving CTF
cryptography challenges.

Here's an example of me using cryptonite to solve
[lowe](https://ctftime.org/writeup/11328) from CSAW Quals 2018:

```python
>>> from cryptonite import *
>>> asn_decode('''MIHdMA0GCSqGSIb3DQEBAQUAA4HLADCBxwKBwQDPcH7tl5AXt/b0dv87plVZrbGC
... 4Hz6IzOx7AVrf3uWEkBU8fV0iwTDaU6Q8Nmf7gWEqHpwgXWA1JOTMhuyCAf/3iWk
... yKvUbZXB43QNnmQf53+bls7K6RjmeiSJUrXaga53Qr2uUbEpJFlzQVBXrnXft1p4
... 6CQ3nlJQZZLDdQ6aHH5wG+6N38epynJTTNOwlXn4ek6zdvkmfNGhbh5XkJXFuG9L
... jyT7YT8Ip+DkddJVVq5ByM7iSOkNrJZdxH3btMUCAQM=''')
[['1.2.840.113549.1.1.1', ''], [1953100985460341348696462250270875098931515807146586756296095446519328460202594322688077959911801412881736536007030245814199784734114468379391959242638228445246656155129859794350223734103552981321896683545886584718379382489138858499065228901412805708175575610007278296746952620830529848517741610397035368508736304074009571123132231492002047409382240786830369954266084929667038697671614351425836882238175963587766360974168461069129309445949172255481878016805287109L, 3]]
>>> n = 1953100985460341348696462250270875098931515807146586756296095446519328460202594322688077959911801412881736536007030245814199784734114468379391959242638228445246656155129859794350223734103552981321896683545886584718379382489138858499065228901412805708175575610007278296746952620830529848517741610397035368508736304074009571123132231492002047409382240786830369954266084929667038697671614351425836882238175963587766360974168461069129309445949172255481878016805287109L
>>> c = 219135993109607778001201845084150602227376141082195657844762662508084481089986056048532133767792600470123444605795683268047281347474499409679660783370627652563144258284648474807381611694138314352087429271128942786445607462311052442015618558352506502586843660097471748372196048269942588597722623967402749279662913442303983480435926749879440167236197705613657631022920490906911790425443191781646744542562221829319509319404420795146532861393334310385517838840775182
>>> k = iroot(3, c + n)
>>> k
12950973085835763560175702356704747094371821722999497961023063926142573092871510801730909790343717206777660797494675328809965345887934044682722741193527531L
>>> k ** 3 == c + n
True
>>> key = int_to_str(k)
>>> key
'\xf7G\t\xad\x02\xfe\x85\xd8\xd3\xf9\x93\xd5\xffW\x16\xea\xbbX)\xdf\r\x12bJ\x04\x8e\nK\xd7&\xa6\xc4(\xa3\xcdZ\xc6$\x89\x00\x1173\xef\xfd\xf1\xdcK\x887 \x9c\x92\xa9\xa3\xe1a\xd0G\x8d\x04\xdb\xd0\xeb'
>>> flag = b64d('kStoynmN5LSniue0nDxli9csSrBgexZ/YOo5e+MUkfJKwvht8hHsYyMGVYzMlOp9sAFBrPCbm4UA4n7oMr2zlg==')
>>> flag
'\x91+h\xcay\x8d\xe4\xb4\xa7\x8a\xe7\xb4\x9c<e\x8b\xd7,J\xb0`{\x16\x7f`\xea9{\xe3\x14\x91\xf2J\xc2\xf8m\xf2\x11\xecc#\x06U\x8c\xcc\x94\xea}\xb0\x01A\xac\xf0\x9b\x9b\x85\x00\xe2~\xe82\xbd\xb3\x96'
>>> xor(key, flag)
'flag{saltstacksaltcomit5dd304276ba5745ec21fc1e6686a0b28da29e6fc}'
```

cryptonite includes:
 * encoding / decoding utilities like `asn_decode`, `int_to_str`, `unhex`, and `b64d`
 * number theory functions like `mod_inv` and `iroot`
 * byte manipulation methods like `xor` and `reverse`
