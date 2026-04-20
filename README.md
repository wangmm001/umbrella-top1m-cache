# umbrella-top1m-cache

Daily snapshots of [Cisco Umbrella Top 1M](https://umbrella.cisco.com/blog/cisco-umbrella-1-million), mirrored by [`wangmm001/feedcache`](https://github.com/wangmm001/feedcache).

## Layout

```
data/
  YYYY-MM-DD.csv.gz     # daily snapshot, gzipped
  current.csv.gz        # pointer to the most recent snapshot
```

File contents are the upstream `top-1m.csv` verbatim: two columns `rank,domain`.

## Consume

```bash
# latest only
curl -L https://raw.githubusercontent.com/wangmm001/umbrella-top1m-cache/main/data/current.csv.gz | zcat | head

# full history
git clone --depth=1 https://github.com/wangmm001/umbrella-top1m-cache.git
```

## License

The data is subject to [Cisco Umbrella's terms of service](https://umbrella.cisco.com/blog/cisco-umbrella-1-million). This repository's `LICENSE` only covers the cron/README scaffolding.

## How it works

A daily GitHub Actions cron calls `wangmm001/feedcache`'s reusable workflow, which downloads and gzips the day's list. No commit is produced when the content hasn't changed.
