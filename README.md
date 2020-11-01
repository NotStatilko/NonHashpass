# NonHashpass

**NonHashpass** is _Password Based Key Derivation Function_ (_PBKDF_) based on **PRNG** and **14** hash-functions.

Your `phrase` (a.k.a `master_key`) concatenates with `unique_word`, `iterations` and passes to **sha512** to create a **initkey**. Initialization key **initialize PRNG** which **shuffles** list with 14 various hash-functions. Initkey passes to the cycled shuffled hash-functions `iteration` times. Last hash **additionaly hashed with shake_256** algorithm, which allow you to get **endless** bytes with sponge function.

**Any** changes to the passed arguments **fully changes order** of hash-functions. Due to this functionality it's **impossible** to create [**ASIC**](https://en.m.wikipedia.org/wiki/Application-specific_integrated_circuit) device.

As a `phrase` i suggest Bitcoin's seed-phrase defined in [**BIP39**](https://en.bitcoin.it/wiki/Seed_phrase).

**Clone NonHashpass:**
```
git clone https://github.com/NotStatilko/NonHashpass
```

**WARNING**: For better security i suggest you to use `iterations` count **starting from 10,000,000**. It may take some time for generating passwords but it will be very extremly hard to brute-force such, even if you have bad `phrase` (a.k.a `master_key`) or it leaked to the attackers. Feel free to set this argument to any number **from 10M to 100M** or even 1 billion. Or even to 100B! Or eve....eh, nevermind. I can talk about this forever.

**Use:**
```
$ python3
>>> from NonHashpass import hashpass
>>>
>>> hashpass('master_key','unique_word',1_000_000).hexdigest(32)
'cc4500ffb508a8c617ae71ff37aba56c1ba48ad02eedb70821e020a243b01961'
```
