# fcvm benchmark raw logs

Large raw logs from fcvm's Chromium benchmark campaigns, kept out of
[ejc3/fcvm](https://github.com/ejc3/fcvm) to keep that repository small. Paths
mirror fcvm's: a file here at `bench/chromium/results/<run>/corpus-access.log`
belongs to the run fcvm keeps at the same path.

fcvm keeps each log's sha256 in the run's `dns-evidence.json` and a pointer in
the run's `external-logs.json` (this repository, the path, and the commit here
that holds the file). fcvm's `bench/chromium/campaign_summary.py` verifies a
run against this repository when `FCVM_BENCH_RECORDS` names a checkout of it,
and refuses the run, saying so, when it does not.

## 2026-10-22/23 corpus campaign

fcvm PR [#1172](https://github.com/ejc3/fcvm/pull/1172), branch
`report/close-not-measured`. The runs' fcvm source revisions are in each run's
`reqbench.jsonl` meta line or `run.json`.

| directory | what | named by an fcvm record |
|---|---|---|
| `bench/chromium/results/reqbench-20261022-corpus-*` (15 serial runs and the throughput run `-s13`) | the corpus replay server's access log (`corpus-access.log`) and DNS log (`corpus-dns.log`) of each run | yes: `dns-evidence.json` (`corpus_access_log_sha256`, `corpus_dns_log_sha256`) and `external-logs.json` |
| `bench/chromium/results/corpusextra-2026102[23]-*` (memory and host-control runs) | the same two logs of those runs | no: no fcvm record names them; kept as raw data |

The access logs hold the requests the captured pages made, query strings
included. Some third-party requests in the captured elmundo.es page carry the
public IP address of the machine that captured the corpus (the same address is
in fcvm's committed `bench/chromium/corpus-live/` bodies). Review that before
making this repository public.
