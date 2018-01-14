# scripts for miners

For these scripts to work, binaries for
[ccminer](https://github.com/tpruvot/ccminer) and
[nheqminer](https://github.com/nicehash/nheqminer) (renamed `eqm`) should be
present in the same directory as the scripts. Be sure to apply the
[patch](./nheqminer_quit_on_eof.patch) to nheqminer!

Be sure to set your appropriate payout address (and other constants, if
applicable) in each of these scripts.

### mining

The [`./bin/multi-mine`](./bin/multi-mine) script mines the most profitable algorithm
with your gpu. You'll need to set the constants defined at the top of the
script, which can come from the benchmarking script.

### benchmarking

The gpu benchmarking script [`./bin/benchmark`](./bin/benchmark) directs
miner output to `./tmp`, which you should manually check to determine your
hashing speed when setting your rates for mining.
