# Mining

For these scripts to work, binaries for
[ccminer](https://github.com/tpruvot/ccminer),
[eqm](https://github.com/nicehash/nheqminer), and
[cpuminer](https://github.com/JayDDee/cpuminer-opt) should be present in the
same directory as the scripts.

Be sure to set your appropriate BTC address (and other constants, if
applicable) in each of these scripts.

### Benchmarking

The gpu benchmarking script [`./gpu-benchmark`](./gpu-benchmark) directs
miner output to `./tmp`, which you should manually check to determine your
hashing speed when setting your rates for mining.

### `nh-profit`

This checks your profitability on nicehash.
```sh
# (this example address isn't mine)
$ nh-profit -a 37aArqRtuUj9znKD1LkSekjpnyJ9AeDhqs
3935.21 USD/day

$ nh-profit -h
Usage: nh-profit [options]
  check your current daily profitability from nicehash

options:
  -a, --addr <ADDR>          Bitcoin address of nicehash provider.
                             (default: 37aArqRtuUj9znKD1LkSekjpnyJ9AeDhqs)
  -c, --currency <CURRENCY>  Currency for output: BTC, USD, GBP, EUR.
                             (default: USD)
  -n, --no-pretty            Displays profitability in less pretty format.
```

You should edit the script and change the default to something more useful.
