# python-signer

Library used for EOSIO signing mechanisms

## Installation

### Supported Python versions
- 3.9.x

### Development

To work on the library during development install using:
```bash
pip install -e .
```

### Production

To install the library for use by a virtual environment use the below installation instructions.

```bash
mkdir -p ~/envs
python3 -m venv ~/envs/eosio-signer 
source ~/envs/eosio-signer/bin/activate
pip install https://github.com/bullish-exchange/python-signer@main
```

## Testing
The tests can be run by using [tox](https://tox.readthedocs.io/en/latest/) or [pytest](https://docs.pytest.org/en/6.2.x/). See the below tox and pytest sections for more information.

### tox

```bash
$ tox

GLOB sdist-make: /git/python-signer/setup.py
py39 inst-nodeps: /git/python-signer/.tox/.tmp/package/1/eosio_signer-develop.zip
py39 installed: attrs==21.2.0,base58==2.1.0,ecdsa==0.17.0,eosio-signer===develop,iniconfig==1.1.1,packaging==21.0,pluggy==0.13.1,py==1.10.0,pyparsing==2.4.7,pytest==6.2.4,six==1.16.0,toml==0.10.2
py39 run-test-pre: PYTHONHASHSEED='2025419556'
py39 run-test: commands[0] | pytest
========================================================= test session starts ==========================================================
platform darwin -- Python 3.9.6, pytest-6.2.4, py-1.10.0, pluggy-0.13.1
cachedir: .tox/py39/.pytest_cache
rootdir: /git/python-signer
collected 8 items                                                                                                                      

tests/test_eosiokey.py ........                                                                                                  [100%]

========================================================== 8 passed in 0.16s ===========================================================
_______________________________________________________________ summary ________________________________________________________________
  py39: commands succeeded
  congratulations :)
```

### pytest

```bash
$ pytest

========================================================= test session starts ==========================================================
platform darwin -- Python 3.9.6, pytest-6.2.4, py-1.10.0, pluggy-0.13.1
rootdir: /git/python-signer
collected 8 items                                                                                                                      

tests/test_eosiokey.py ........                                                                                                  [100%]

========================================================== 8 passed in 0.17s ===========================================================
```


## Examples

Examples can be found in the [examples](./examples) directory. 

### Generate new keys
```python
from eosio_signer import EOSIOKey
import hashlib

# create key

# This is for instructional purposes. 
# This is not an endorsement to use this library to generate keys.
k = EOSIOKey()

print(f"private key: {k.to_wif()}")
print(f"public key:  {k.to_public()}")
```

### Import/Sign
```python
from eosio_signer import EOSIOKey
import hashlib

digest = hashlib.sha256("digest".encode()).hexdigest()

# import key
# DO NOT USE these keys as they are known keys that are publicly available 
r1_key = EOSIOKey('PVT_R1_2sTZXHRWPfgWfn4gTD4bXjVsKRTSYBCekebBgJq1P9SW7ckoXk')
k1_key = EOSIOKey('PVT_K1_r9seSVdS9yTRmSXtLrpELLZ5dhbEqr12jLCRg5NJAWr5q8U9o')

# r1 signing
r1_sig = r1_key.sign(digest)

# k1 signing
k1_sig = k1_key.sign(digest)

print(f'r1_sig: {r1_sig}')
print(f'k1_sig: {k1_sig}')
```