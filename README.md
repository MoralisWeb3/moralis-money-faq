# How do filters work?

## 🕚 Coin Age

Measures the time since the coin was minted.

## 💸 Buyers

Measures how many new addresses bought the coin during the specified time-frame.

Any address who has zero coins and uses a DEX to buy some coins during the specified time-frame is counted as a buyer.

## 💸👴 Experienced Buyers

Same as Buyers with the additional requirement that the address needs to have at least 100 outgoing transactions to be qualified.

(we are working on adding additional requirements such as the age of the address)

## 💦 Liquidity

Measures how much liquidity changed during the specified time-frame.

## 💎 Holders

Measures how much holders changed during the specified time-frame.
