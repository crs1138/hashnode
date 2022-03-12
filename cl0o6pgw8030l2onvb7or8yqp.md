## Transferring BTC from Binance to Ledger wallet

I have finished the investment part of my strategy buying BTC on Binance. I have also recently got a new Ledger wallet. I could see that the price of BTC has dropped by 50% in the last 2 months (Nov 21—Jan 22), so I estimated it would take another at least two months before it would reach the price level where I'm going to be ready to sell. What a great opportunity to learn moving BTC between Binance and my Ledger, whilst keeping the BTC *safer*. Here's my learning.

## Technicalities of the transfer from Binance to Ledger

#### Withdrawing BTC

1. Go to Ledger Live BTC account (Segwit) and click the *Recieve* button.
2. Click *Continue* in the modal that pops up.
3. Connect Ledger device.
4. Open the *Bitcoin app* on the device.
5. Copy the public key for the wallet.
6. Go to Binance >> Wallets >> Fiat&Spot
7. In the *Select Coin* input, type in *BTC*
8. Select *Withdraw to new address* (no point saving the address as [Ledger's BTC public key is regenerated](https://support.ledger.com/hc/en-us/articles/360034336713-Receiving-address-changed?support=true) after each successful transaction)
9. Paste in the public key from Ledger. The network is selected automatically.
10. Fill in the amount and click *Submit*.
11. Authorise the transaction using the email, SMS and authenticator codes.

### Ledger side

Ledger offered me two kinds of BTC accounts: Native Segwit and Taproot. The Native Segwit is the one that has been used up until recently when it got soft-forked and Ledger is now pushing Taproot. It is supposed to be more private and more performant. More information is provided at Ledger's webpage about [creating the BTC Taproot account in Ledger Live](https://support.ledger.com/hc/en-us/articles/4410908103185-Creating-a-Bitcoin-Taproot-account-in-Ledger-Live?docs=true).

I had the *Native Segwit* BTC account as it comes with the Ledger wallet by default. After reading about the update, I decided to try the *Taproot* out. I've made a new account whilst keeping the Segwit one alongside the new one. That was a smart decision.

### Binance side

When I tried that (22/1/22) Binance would not accept the *Taproot* address. It just would not let me use it. So I ended up using the *Segwit* one.

## Cost of the transaction

The whole operation ended up a little pricey. I was transferring an amount in the nominal value of a few hundred dollars. Binance charges a flat fee of **0.0005 BTC** for withdrawals in this price bracket. This seemed a bit steep to me. The BTC-USDT exchange rate today was extremely low due to the recent sudden drop of BTC to roughly $34,600.

```
Binance - withdrawing 0.0095251 BTC
Fee: 0.0005 BTC ~ $17.30
===
Ledger: received 0.0090251 BTC

```

#### Alternative – using LTC as the middle step

I thought this was a bit steep price to pay. So, I found another [solution](https://www.reddit.com/r/binance/comments/kttxs6/how_to_cheaply_withdraw_from_binance/). It turns out that Binance charges significantly less for withdrawing alt-coins such as LTC and then exchanging it back to BTC in the receiving wallet. The fee is only 0.001 LTC (1 LTC ~ $106.5). This might work when employed with another wallet. With Ledger, however, it's a false economy and I wish I was able to find out the cost of exchange from LTC back to BTC before trying this out. [Ledger's fees](https://support.ledger.com/hc/en-us/articles/360021039173-Choose-network-fees?docs=true) are based on the speed of the transaction and represent the reward a miner receives for processing the transaction into the blockchain.

* **High:** the transaction will roughly be included in the next block (about 10 min for Bitcoin)
* **Standard:** the transaction will roughly be included within 3 blocks (about 30 min for Bitcoin)
* **Low:** the transaction will roughly be included within 6 blocks (about 60 min for Bitcoin)

As I wrote above, I did not find a way to predict exactly how much this would be before starting the operation. So I just went with it and took this as the cost of learning.

```
Binance - exchange 0.0095251 BTC => 3.09550969 LTC
Binance - withdrawing 3.09550969 LTC
Fee: 0.001 LTC ~ $0.1065
===
Ledger - received 3.09450743 LTC
Fee (low speed): 0.00000226 LTC
BTC received: 0.00925157 BTC
BTC after the transaction was verified by mines: 0.00873473 BTC
===

BTC  0.0095251
BTC -0.00873473
===
Costs: 0,00079037 BTC ~ $27,346802 :(
```

## Conclusion

Next time, I gotta try using the Binance default withdrawal mechanism to verify the total price of the transaction. For now, it seems that it is better to do it that way.