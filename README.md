# libor-oracle
Libor DAO oracle

### Publish package
`sui client publish --gas-budget 10000`

Result:
```
----- Certificate ----
Transaction Hash: 8KXgVbC+wtFPc4L9sGrMNM++KZ4avmBge7Yd6hy+cpM=
Transaction Signature: AA==@fWwr7yx7W2mNMxs9rpkXHkkQkhFAM81buS2sLnoClfoCtJ84TKogmbrRFTuWBHp8ebSTse7MNjo1iz58zQ8TAA==@WBoJwkIBNBN0u8lbvDXrE8t7UQqNq/56vcbCUuy49hc=
Signed Authorities Bitmap: RoaringBitmap<[0, 2, 3]>
Transaction Kind : Publish
----- Transaction Effects ----
Status : Success
Created Objects:
  - ID: 0x1723b683948472b797daf88ca13ee8eea2201ad8 , Owner: Immutable
Mutated Objects:
  - ID: 0xdc54d85e3277f5ff62f47dd7fc4c4b763bce2f5b , Owner: Account Address ( 0x163c989a48eb685309dcd1d75363aab439c8aeb0 )
```

* Package: `0x1723b683948472b797daf88ca13ee8eea2201ad8`


### Add USDT to oracle:
* Type Arguments: `<addr>::<module>::<type>` get from the deployed token package: [sui_ft_token](https://github.com/Libor-DAO/sui-ft-token)
```
export PACKAGE=0x1723b683948472b797daf88ca13ee8eea2201ad8
sui client call --gas-budget 10000 --package $PACKAGE --module "oracle" --function "new_oracle" --type-args 0xc99a286ab0d12312cbc2ceec6ce5dc196d4721a2::usdt::USDT --args 9
```

Result:
```
----- Certificate ----
Transaction Hash: 1Ug0PK1yeHIt496+02MjjnbkIHx5O6kVrFo9IT6xNb8=
Transaction Signature: AA==@5pP5m60vVoIjSKhYlJ7QJCyGk5xcxJf+g4uNLEIM+ARjd+ZSyPmz4i82ID5GyEq7IILDz8oZmfhwv5ruxXnnDQ==@WBoJwkIBNBN0u8lbvDXrE8t7UQqNq/56vcbCUuy49hc=
Signed Authorities Bitmap: RoaringBitmap<[0, 2, 3]>
Transaction Kind : Call
Package ID : 0x1723b683948472b797daf88ca13ee8eea2201ad8
Module : oracle
Function : new_oracle
Arguments : [9]
Type Arguments : ["0xc99a286ab0d12312cbc2ceec6ce5dc196d4721a2::usdt::USDT"]
----- Transaction Effects ----
Status : Success
Created Objects:
  - ID: 0x0348c78eb509aaa8aa75b2e0903bdb286f2f9366 , Owner: Account Address ( 0x163c989a48eb685309dcd1d75363aab439c8aeb0 )
  - ID: 0xf9b05701e84d595971d4911c770d655546408db3 , Owner: Shared
Mutated Objects:
  - ID: 0xdc54d85e3277f5ff62f47dd7fc4c4b763bce2f5b , Owner: Account Address ( 0x163c989a48eb685309dcd1d75363aab439c8aeb0 )
```

* USDT oracle: `0xf9b05701e84d595971d4911c770d655546408db3`
* USDT oracle key: `0x0348c78eb509aaa8aa75b2e0903bdb286f2f9366`

### Update price USDT in oracle:
```
export PACKAGE=0x1723b683948472b797daf88ca13ee8eea2201ad8
export ORACLE_USDT=0xf9b05701e84d595971d4911c770d655546408db3
export ORACLE_USDT_KEY=0x0348c78eb509aaa8aa75b2e0903bdb286f2f9366
export USDT_PRICE=1000000000
export CURRENT_TS_MS=1670412895815 # Current timestamp
sui client call --gas-budget 10000 --package $PACKAGE --module "oracle" --function "update" --type-args 0xc99a286ab0d12312cbc2ceec6ce5dc196d4721a2::usdt::USDT --args $ORACLE_USDT $ORACLE_USDT_KEY $USDT_PRICE $CURRENT_TS_MS
```

Result:
```
----- Certificate ----
Transaction Hash: TX2fAadevupNQlNtUbmCOl5Y96SHdmIvRIwwIH0vu0o=
Transaction Signature: AA==@DIGg6w6rOl6C2qZZseIK1/IVYv3GLgS3+K5MsvNjF24UkIGr12j1IgwgYpdWKufVYhqE99EzEedeoGNgs3qkAw==@WBoJwkIBNBN0u8lbvDXrE8t7UQqNq/56vcbCUuy49hc=
Signed Authorities Bitmap: RoaringBitmap<[1, 2, 3]>
Transaction Kind : Call
Package ID : 0x1723b683948472b797daf88ca13ee8eea2201ad8
Module : oracle
Function : update
Arguments : ["0xf9b05701e84d595971d4911c770d655546408db3", "0x348c78eb509aaa8aa75b2e0903bdb286f2f9366", 1000000000, 1670412895815]
Type Arguments : ["0xc99a286ab0d12312cbc2ceec6ce5dc196d4721a2::usdt::USDT"]
----- Transaction Effects ----
Status : Success
Mutated Objects:
  - ID: 0x0348c78eb509aaa8aa75b2e0903bdb286f2f9366 , Owner: Account Address ( 0x163c989a48eb685309dcd1d75363aab439c8aeb0 )
  - ID: 0xdc54d85e3277f5ff62f47dd7fc4c4b763bce2f5b , Owner: Account Address ( 0x163c989a48eb685309dcd1d75363aab439c8aeb0 )
  - ID: 0xf9b05701e84d595971d4911c770d655546408db3 , Owner: Shared
```

## New unix time
```
export PACKAGE=0x7c68078128c0d0369a763c88a1d7164619d09212
sui client call --gas-budget 10000 --package $PACKAGE --module "unix_time" --function "new_time"
```

Result:
```
Transaction Hash: GVvodVlWpPuk/fe79UKpe+aUiTG5r0T9q04lmr4J794=
Transaction Signature: AA==@cbMJDA2fAw1GF/1ybbqIYAQVQ9Gn2+LB8giJ3aBaS4Jh1/OUDkD2ukhTg4ON9IVtSb2q0+1mCW5jPFrZjlHBAg==@WBoJwkIBNBN0u8lbvDXrE8t7UQqNq/56vcbCUuy49hc=
Signed Authorities Bitmap: RoaringBitmap<[0, 1, 2]>
Transaction Kind : Call
Package ID : 0x7c68078128c0d0369a763c88a1d7164619d09212
Module : unix_time
Function : new_time
Arguments : []
Type Arguments : []
----- Transaction Effects ----
Status : Success
Created Objects:
  - ID: 0x29f65c057068175d78c0730ee8b1671a9393f752 , Owner: Account Address ( 0x163c989a48eb685309dcd1d75363aab439c8aeb0 )
  - ID: 0xd9d77209e345d6957868f3be26d5ac1e33d4de7c , Owner: Shared
Mutated Objects:
  - ID: 0xdc54d85e3277f5ff62f47dd7fc4c4b763bce2f5b , Owner: Account Address ( 0x163c989a48eb685309dcd1d75363aab439c8aeb0 )
```
* Unix time key: `0x29f65c057068175d78c0730ee8b1671a9393f752`
* Unix time: `0xd9d77209e345d6957868f3be26d5ac1e33d4de7c`

## Update time
```
export PACKAGE=0x7c68078128c0d0369a763c88a1d7164619d09212
export UNIX_TIME_KEY=0x29f65c057068175d78c0730ee8b1671a9393f752
export UNIX_TIME=0xd9d77209e345d6957868f3be26d5ac1e33d4de7c
export CURRENT_TS_MS=1670412895815 # Current timestamp
sui client call --gas-budget 10000 --package $PACKAGE --module "unix_time" --function "update" --args $UNIX_TIME $UNIX_TIME_KEY $CURRENT_TS_MS
```
Result:
```
----- Certificate ----
Transaction Hash: I4+HiHKoVeobpUCSo23bVcrImJKtLt7y6AP/4/2nhkM=
Transaction Signature: AA==@XTvmuE/lJzq2GV9sqVVdlUM26XodTeVyekSnXe2fc+T0CUjMhhXZ4QTcJySfUtGAY5Ma7pATCUt2ZgaUlZLiAA==@WBoJwkIBNBN0u8lbvDXrE8t7UQqNq/56vcbCUuy49hc=
Signed Authorities Bitmap: RoaringBitmap<[0, 2, 3]>
Transaction Kind : Call
Package ID : 0x7c68078128c0d0369a763c88a1d7164619d09212
Module : unix_time
Function : update
Arguments : ["0xd9d77209e345d6957868f3be26d5ac1e33d4de7c", "0x29f65c057068175d78c0730ee8b1671a9393f752", 1670412895815]
Type Arguments : []
----- Transaction Effects ----
Status : Success
Mutated Objects:
  - ID: 0x29f65c057068175d78c0730ee8b1671a9393f752 , Owner: Account Address ( 0x163c989a48eb685309dcd1d75363aab439c8aeb0 )
  - ID: 0xd9d77209e345d6957868f3be26d5ac1e33d4de7c , Owner: Shared
  - ID: 0xdc54d85e3277f5ff62f47dd7fc4c4b763bce2f5b , Owner: Account Address ( 0x163c989a48eb685309dcd1d75363aab439c8aeb0 )
```