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

# Roadmap

1. Get coins with higher/lower marketcap than X
2. Get coins with higher/lower volume than X in a specified time-frame
3. Experienced Traders - addresses that have proven trading track-record
4. Filters based on % of supply locked/% of LP tokens locked
5. Savings filters and getting email alerts for filters
