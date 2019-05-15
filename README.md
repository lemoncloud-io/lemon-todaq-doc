# lemon-todaq-doc

Restfull Micro-Service to support general commerce above TodaQ block-chain technology.

# Objective

- Support general commerce payment based on [TodaQ API](https://todaqfinance.com/)
- Ready to deploy in AWS Cloud in 3 minutes.
- Provide a web based admin console for payment management.
- Agent module in nodejs, python for developer.


# Requirements

![TodaQ for commerce](assets/lemon-todaq.png)


## 유저 (User)

- TYPE: `ACCOUNT`
- Master information about user(or company), which is copied via RDB.
- Encrypt TODAQ's Account Information like `<account-id>`. (Only `super` user can see).
- Can be synchronized with TODAQ Accounts.
- `total` has total amount of value of conins belonged to user.

1. `연결(link)`: Connect current user with TODAQ's Account (or create new one)
    - `Account Type`: BIZ/INV
    - `Account ID`: save the encrypted todaq's account-id into KMS.

1. `활성(activate)`: Change `active` state in TODAQ.
    - `Active State`: ...

1. `동기화(sync)`: Synchronize information, and aggregate total value of coins.
    - `Balance`: total balance of coins.
    - `Sync Date`: timestamp of synchronization (including webhook callback).

1. `패스코드(passcode)`: Confirm the transaction per account/enterprise.
    - `Digit Code`: 4~6 digits number.


## 동전 (Coin)

- TYPE: `COIN`
- Like coins in real-world, it has value estimation as 10 KRW, 100 KRW
- Can be matched with TODAQ's `<file-type-id>` attribute.
- Only define the specifications (like 10KRW) about each coin.

1. `발행(issue)`: Generate coins like exchange-bank in real world (but, enterprisor has ownership)
    - `Coin Name`: SOM/KRW/...
    - `Minimum Value`: 10 SOM
    - `Coin ID`: same as `<file-id>`
    - `Issue Reason`: ...

1. `폐기(trash)`: Trash coins only by Owner.
    - `Trash Account`: ...

1. `교환(exchange)`: Exchange between different conins with same value. (Use transaction api internally)
    - `Exchange Rate`: 10 SOM = 10 KRW.
    - `Exchange Cost`: as tax per exchange (or zero) to enterprise.

1. `전달(transfer)`: Transfer coins to other account w/ transaction.
    - `Transfer Rate`: Y := X + a
    - `Transfer Cost`: as tax per transfer. (or zero)  to enterprise.


## 결제 (Payment)

- TYPE: `PAYMENT`
- Use coins to buy something. (and get some changes)
- Make transaction, and make sure settlement in seconds. (TBD)

1. `결제(pay)`: Transfer coins in total cost of product to seller, then get the changes.
    - `meta`: save product's id.
    - `transaction-id`: keep track of transaction-id in database (will be synced with todaq-api)

1. `취소(cancel)`: Cancel payment, then returns back product/coins.
    - `transaction-id`: keep the original transaction-id.

1. `충전(charge)`: Buying coins with PG payment from enterprise.
    - `Payment Code`: ...

1. `환불(refund)`: Refund to credit.



## 쿠폰 (Coupon)

- TYPE: `COUPON`
- Like coins in real-world, it has the benefit like 10% discount if total > 1000.
- Rule based definitions.

1. `발행(issue)`: Provider could generate.
    - `Serial Code`: ...

1. `수락(accept)`: Provider could generate.
    - ``: ...



--------------------
# CHECK THIS #

- [ ] search files by `<file-type-id>`? or scan all files per acount in order to aggregate?
    - 'Accounts - Get File Types' -> 'Accounts - Get Files by Type'
- [ ] define each state of `file(coin)`, `transaction`.
- [ ] size of meta data in file. purpose of meta history?
- [ ] use-case of 'Files Proofs'
- [ ] implementing of TodaQ app.
- [ ] search maximum limit/page number.
- [ ] common error handling 

