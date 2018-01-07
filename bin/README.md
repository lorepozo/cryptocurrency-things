## scripts for owners of some cryptocurrencies

All of these scripts require [`jq`](https://stedolan.github.io/jq).

All of these scripts require running a node of some kind.

### balance

There are five balance commands, one each for bitcoin, litecoin, ethereum,
zcash, and all four. Each of these require the corresponding nodes to be
running locally (so commands to each cli should work). The per-currency
commands, `bbalance`, `lbalance`, `ebalance`, and `zbalance`, take form at
follows:

```sh
$ bbalance
0.00000000 16Ah3DLDFZTc2UMCkEDbH7uXySFFp7qDpw
0.00000000 1NvHCNcd6xrAWKq5MwAk4LXB39cDsp9pNj
0.01030460 17gsVY9ZFA3jMHUB2XxbfqrKVMwxF1ZD1Q
0.18157804 1D4hQVBvwe5M1egXoWju6Chutv5C3Ly6Fy
1.54731878 18TD3QtGjQiBcgtz4TWTAk4HvtYJ9nsj6V
```

These commands only show information for addresses you have private keys
for. The overall command, `balance`, looks as follows:

```sh
$ balance
BITCOIN: 1.73920142
0.00000000 16Ah3DLDFZTc2UMCkEDbH7uXySFFp7qDpw
0.00000000 1NvHCNcd6xrAWKq5MwAk4LXB39cDsp9pNj
0.01030460 17gsVY9ZFA3jMHUB2XxbfqrKVMwxF1ZD1Q
0.18157804 1D4hQVBvwe5M1egXoWju6Chutv5C3Ly6Fy
1.54731878 18TD3QtGjQiBcgtz4TWTAk4HvtYJ9nsj6V

LITECOIN: 11.00751980
11.00751980 LQm1rLT3WzW38d8Udj4ntErV5mRgEqJk5U

ETHEREUM: 2.01532351
2.01532351 0xe81E250b08b6A0527ebda13EfB252Fa901A2e67a

ZCASH: 9.19730801
0.00000000 t1bc3Z5V4nskqNQvJt24GnsPRWkS2yAE4aY
7.16729381 t1fadkoKDuFg8DHu1XSGt87U8tCiz2CLhfb
2.03001420 zcAXJxTcq1ewPwDq4wDYVEChrP5jLWWVJwADVL6AwVPUtTHThWPFh8a3RQdbQJm7BhFzcWPzzwuq1JjtjAurGbRVsbAxobL
```

### received transactions

There are three scripts for getting transactions that have been received:
`br`, `lr`, and `zr` (corresponding to bitcoin, litecoin, and zcash
respectively). Each of these require the corresponding nodes to be running
locally (so commands to each cli should work). Each transaction occupies one
line, so it's useful for scripting with `diff`.

```sh
$ br
{"time":"2017-07-17 19:18:29","amount":0.32680289,"address":"13G23badvUrMJzorWRcjT74grGRLPeFYrS"}
{"time":"2017-07-22 00:03:39","amount":0.14756864,"address":"13G23badvUrMJzorWRcjT74grGRLPeFYrS"}
{"time":"2017-08-23 03:15:35","amount":-0.01125,"address":"1CfvcuUpJ6q1TgXS1bfEncTC2Jk5wznkGi"}
{"time":"2017-08-23 15:06:03","amount":-0.01125,"address":"1CfvcuUpJ6q1TgXS1bfEncTC2Jk5wznkGi"}

# zcash transactions can also show a memo
$ zr
{"time":"2017-04-03 08:08:17","amount":0.89187791,"memo":null,"address":"zcAXJxTcq1ewPwDq4wDYVEChrP5jLWWVJwADVL6AwVPUtTHThWPFh8a3RQdbQJm7BhFzcWPzzwuq1JjtjAurGbRVsbAxobL"}
{"time":"2017-04-03 13:03:18","amount":2.1481052,"memo":"make it all private!","address":"zcAXJxTcq1ewPwDq4wDYVEChrP5jLWWVJwADVL6AwVPUtTHThWPFh8a3RQdbQJm7BhFzcWPzzwuq1JjtjAurGbRVsbAxobL"}
```

### market summaries

The script `ccsummary` shows a summary of your values according to the
current market. See configurability by looking for the `XXX` comments in the
code (three statements may need to be adjusted by you). There are three ways
of using it directly:

```sh
# get a simple JSON document with usd values of your holdings
$ ccsummary
{
  "btc": 7270.28,
  "bch": 975.01,
  "ltc": 775.47,
  "zec": 4316.47,
  "eth": 9217.13
}

# get a plain text summary of your holdings
$ ccsummary p
2017-09-10 13:49:21
   1.68809312 BTC $4307.00 -> $7270.62
   1.68396028 BCH  $579.00 -> $975.01
  11.00741980 LTC   $70.52 -> $776.24
  19.16644441 ZEC  $225.21 -> $4316.47
  30.57802442 ETH  $301.48 -> $9218.66
  $22557.01

# get a similar level of expressivity in a JSON document
$ ccsummary j
{
  "time": "2017-09-10 13:46:47",
  "data": {
    "btc": {
      "amount": 1.68809312,
      "price": 4297.8,
      "as_usd": 7255.086611136
    },
    "bch": {
      "amount": 1.68396028,
      "price": 578.6,
      "as_usd": 974.339418008
    },
    "ltc": {
      "amount": 11.0074198,
      "price": 70.46,
      "as_usd": 775.5827991079999
    },
    "zec": {
      "amount": 19.16644441,
      "price": 225.2,
      "as_usd": 4316.2832811319995
    },
    "eth": {
      "amount": 30.57802442,
      "price": 300.97,
      "as_usd": 9203.0680096874
    }
  }
}
```

Here's a useful script using `ccsumary` and `jq` to produce some small plain
text output:

```sh
$ ccsummary | jq -r '
  reduce (
    to_entries | sort_by(.value) | reverse | .[] |
    "\n\(.key): $\(.value)"
  ) as $i (
    "total: $\(add)";
    .+$i
  ) '
total: $22584.94
eth: $9234.56
btc: $7276.36
zec: $4318.01
bch: $978.01
ltc: $778
```
