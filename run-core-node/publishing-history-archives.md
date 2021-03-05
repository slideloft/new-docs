---
title: Publishing History Archives
order: 50
---

# publishing history archives

If you want to run a [Full Validator](index.md#full-validator) or an [Archiver](index.md#archiver), you need to set up your node to publish a history archive. You can host an archive using a blob store such as Amazon's s3 or Digital Ocean's spaces, or you can simply serve a local archive directly via an HTTP server such as Nginx or Apache. If you're setting up a [Watcher](index.md#watcher) or a [Basic Validator](index.md#basic-validator), you can skip this section. No matter what kind of node you're planning to run, make sure to set it up to `get` history, which is covered in [Configuration](configuring.md).

## Caching and History Archives

You can significantly reduce the data transfer costs associated with running a public History archive by using common caching techniques or a CDN.

Three simple rules apply to caching the History archives:

* Do not cache the archive state file `.well-known/history-bantu.json` \(**"Cache-Control: no-cache"**\)
* Do not cache HTTP 4xx responses \(**"Cache-Control: no-cache"**\)
* Cache everything else for as long as possible \(**&gt; 1 day**\)

## Local History Archive Using nginx

To publish a local history archive using nginx:

* Add a history configuration stanza to your `/etc/bantu/bantu-core.cfg`:

```text
[HISTORY.local]
get="cp /mnt/xvdf/bantu-core-archive/node_001/{0} {1}"
put="cp {0} /mnt/xvdf/bantu-core-archive/node_001/{1}"
mkdir="mkdir -p /mnt/xvdf/bantu-core-archive/node_001/{0}"
```

* Run new-hist to create the local archive

`# sudo -u bantu bantu-core --conf /etc/bantu/bantu-core.cfg new-hist local`

This command creates the history archive structure:

```text
# tree -a /mnt/xvdf/bantu-core-archive/
/mnt/xvdf/bantu-core-archive
└── node_001
    ├── history
    │   └── 00
    │       └── 00
    │           └── 00
    │               └── history-00000000.json
    └── .well-known
        └── bantu-history.json

6 directories, 2 files
```

* Configure a virtual host to serve the local archive \(Nginx\)

```text
server {
  listen 80;
  root /mnt/xvdf/bantu-core-archive/node_001/;

  server_name history.example.com;

  # default is to deny all
  location / { deny all; }

  # do not cache 404 errors
  error_page 404 /404.html;
  location = /404.html {
    add_header Cache-Control "no-cache" always;
  }

  # do not cache history state file
  location ~ ^/.well-known/bantu-history.json$ {
    add_header Cache-Control "no-cache" always;
    try_files $uri;
  }

  # cache entire history archive for 1 day
  location / {
    add_header Cache-Control "max-age=86400";
    try_files $uri;
  }
}
```

## Amazon S3 History Archive

To publish a history archive using Amazon S3:

* Add a history configuration stanza to your `/etc/bantu/bantu-core.cfg`:

```text
[HISTORY.s3]
get='curl -sf http://history.example.com/{0} -o {1}' # Cached HTTP endpoint
put='aws s3 cp --region us-east-1 {0} s3://bucket.name/{1}' # Direct S3 access
```

* Run new-hist to create the s3 archive

`# sudo -u bantu bantu-core --conf /etc/bantu/bantu-core.cfg new-hist s3`

* Serve the archive using an Amazon S3 static site
* Optionally place a reverse proxy and CDN in front of the S3 static site

```text
server {
  listen 80;
  root /srv/nginx/history.example.com;
  index index.html index.htm;

  server_name history.example.com;

  # use google nameservers for lookups
  resolver 8.8.8.8 8.8.4.4;

  # bucket.name s3 static site endpoint
  set $s3_bucket "bucket.name.s3-website-us-east-1.amazonaws.com";

  # default is to deny all
  location / { deny all; }

  # do not cache 404 errors
  error_page 404 /404.html;
  location = /404.html {
    add_header Cache-Control "no-cache" always;
  }

  # do not cache history state file
  location ~ ^/.well-known/bantu-history.json$ {
    add_header Cache-Control "no-cache" always;
    proxy_intercept_errors on;
    proxy_pass  http://$s3_bucket;
    proxy_read_timeout 120s;
    proxy_redirect off;
    proxy_buffering off;
    proxy_set_header        Host            $s3_bucket;
    proxy_set_header        X-Real-IP       $remote_addr;
    proxy_set_header        X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header        X-Forwarded-Proto $scheme;
  }

  # cache history archive for 1 day
  location / {
    add_header Cache-Control "max-age=86400";
    proxy_intercept_errors on;
    proxy_pass  http://$s3_bucket;
    proxy_read_timeout 120s;
    proxy_redirect off;
    proxy_buffering off;
    proxy_set_header        Host            $s3_bucket;
    proxy_set_header        X-Real-IP       $remote_addr;
    proxy_set_header        X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header        X-Forwarded-Proto $scheme;
  }
}
```

## Backfilling a history archive

Given the choice, it's best to configure your history archive prior to your node's initial synch to the network. That way your validator's history publishes as you join/synch to the network.

However, if you have _not_ published an archive during the node's initial synch, it's still possible to use the [bantu-archivist](https://github.com/bantu/go/tree/master/tools/bantu-archivist) command line tool to mirror, scan, and repair existing archives.

Using the [BBF package repositories](https://github.com/bantu/packages) you can install `bantu-archivist` by running `apt-get install bantu-archivist`

The steps required to create a History archive for an existing validator — in other words, to upgrade a Basic Validator to a Full Validator — are straightforward:

* Stop your bantu-core instance \(`systemctl stop bantu-core`\)
* Configure a history archive for the new node

```text
[HISTORY.local]
get="cp /mnt/xvdf/bantu-core-archive/node_001/{0} {1}"
put="cp {0} /mnt/xvdf/bantu-core-archive/node_001/{1}"
mkdir="mkdir -p /mnt/xvdf/bantu-core-archive/node_001/{0}"
```

* Run new-hist to create the local archive

`# sudo -u bantu bantu-core --conf /etc/bantu/bantu-core.cfg new-hist local`

This command creates the History archive structure:

```text
# tree -a /mnt/xvdf/bantu-core-archive/
/mnt/xvdf/bantu-core-archive
└── node_001
    ├── history
    │   └── 00
    │       └── 00
    │           └── 00
    │               └── history-00000000.json
    └── .well-known
        └── bantu-history.json

6 directories, 2 file
```

* Start your bantu Core instance \(`systemctl start bantu-core`\)
* Allow your node to join the network and watch it start publishing a few checkpoints to the newly created archive

```text
2019-04-25T12:30:43.275 GDUQJ [History INFO] Publishing 1 queued checkpoints [16895-16895]: Awaiting 0/0 prerequisites of: publish-000041ff
```

At this stage your validator is successfully publishing its history, which enables other users to join the network using your archive \(although it won't allow them to `CATCHUP_COMPLETE=true` as the archive only has partial network history\).

## Complete History Archive

If you decide to publish a complete archive — which enables other users to join the network from the genesis ledger — it's also possible to use `bantu-archivist` to add all missing history data to your partial archive, and to verify the state and integrity of your archive. For example:

```text
# bantu-archivist scan file:///mnt/xvdf/bantu-core-archive/node_001
2019/04/25 11:42:51 Scanning checkpoint files in range: [0x0000003f, 0x0000417f]
2019/04/25 11:42:51 Checkpoint files scanned with 324 errors
2019/04/25 11:42:51 Archive: 3 history, 2 ledger, 2 transactions, 2 results, 2 scp
2019/04/25 11:42:51 Scanning all buckets, and those referenced by range
2019/04/25 11:42:51 Archive: 30 buckets total, 30 referenced
2019/04/25 11:42:51 Examining checkpoint files for gaps
2019/04/25 11:42:51 Examining buckets referenced by checkpoints
2019/04/25 11:42:51 Missing history (260): [0x0000003f-0x000040ff]
2019/04/25 11:42:51 Missing ledger (260): [0x0000003f-0x000040ff]
2019/04/25 11:42:51 Missing transactions (260): [0x0000003f-0x000040ff]
2019/04/25 11:42:51 Missing results (260): [0x0000003f-0x000040ff]
2019/04/25 11:42:51 No missing buckets referenced in range [0x0000003f, 0x0000417f]
2019/04/25 11:42:51 324 errors scanning checkpoints
```

As you can tell from the output of the `scan` command, some history, ledger, transactions, and results are missing from the local history archive.

You can repair the missing data using bantu-archivist's `repair` command combined with a known full archive — such as the BBF public history archive:

`# bantu-archivist repair http://history.bantu.org/prd/core-testnet/core_testnet_001/ file:///mnt/xvdf/bantu-core-archive/node_001/`

```text
2019/04/25 11:50:15 repairing http://history.bantu.org/prd/core-testnet/core_testnet_001/ -> file:///mnt/xvdf/bantu-core-archive/node_001/
2019/04/25 11:50:15 Starting scan for repair
2019/04/25 11:50:15 Scanning checkpoint files in range: [0x0000003f, 0x000041bf]
2019/04/25 11:50:15 Checkpoint files scanned with 244 errors
2019/04/25 11:50:15 Archive: 4 history, 3 ledger, 263 transactions, 61 results, 3 scp
2019/04/25 11:50:15 Error: 244 errors scanning checkpoints
2019/04/25 11:50:15 Examining checkpoint files for gaps
2019/04/25 11:50:15 Repairing history/00/00/00/history-0000003f.json
2019/04/25 11:50:15 Repairing history/00/00/00/history-0000007f.json
2019/04/25 11:50:15 Repairing history/00/00/00/history-000000bf.json
...
2019/04/25 11:50:22 Repairing ledger/00/00/00/ledger-0000003f.xdr.gz
2019/04/25 11:50:23 Repairing ledger/00/00/00/ledger-0000007f.xdr.gz
2019/04/25 11:50:23 Repairing ledger/00/00/00/ledger-000000bf.xdr.gz
...
2019/04/25 11:51:18 Repairing results/00/00/0e/results-00000ebf.xdr.gz
2019/04/25 11:51:18 Repairing results/00/00/0e/results-00000eff.xdr.gz
2019/04/25 11:51:19 Repairing results/00/00/0f/results-00000f3f.xdr.gz
...
2019/04/25 11:51:39 Repairing scp/00/00/00/scp-0000003f.xdr.gz
2019/04/25 11:51:39 Repairing scp/00/00/00/scp-0000007f.xdr.gz
2019/04/25 11:51:39 Repairing scp/00/00/00/scp-000000bf.xdr.gz
...
2019/04/25 11:51:50 Re-running checkpoing-file scan, for bucket repair
2019/04/25 11:51:50 Scanning checkpoint files in range: [0x0000003f, 0x000041bf]
2019/04/25 11:51:50 Checkpoint files scanned with 5 errors
2019/04/25 11:51:50 Archive: 264 history, 263 ledger, 263 transactions, 263 results, 241 scp
2019/04/25 11:51:50 Error: 5 errors scanning checkpoints
2019/04/25 11:51:50 Scanning all buckets, and those referenced by range
2019/04/25 11:51:50 Archive: 40 buckets total, 2478 referenced
2019/04/25 11:51:50 Examining buckets referenced by checkpoints
2019/04/25 11:51:50 Repairing bucket/57/18/d4/bucket-5718d412bdc19084dafeb7e1852cf06f454392df627e1ec056c8b756263a47f1.xdr.gz
2019/04/25 11:51:50 Repairing bucket/8a/a1/62/bucket-8aa1624cc44aa02609366fe6038ffc5309698d4ba8212ef9c0d89dc1f2c73033.xdr.gz
2019/04/25 11:51:50 Repairing bucket/30/82/6a/bucket-30826a8569cb6b178526ddba71b995c612128439f090f371b6bf70fe8cf7ec24.xdr.gz
...
```

A final scan of the local archive confirms that it has been successfully repaired

`# bantu-archivist scan file:///mnt/xvdf/bantu-core-archive/node_001`

```text
2019/04/25 12:15:41 Scanning checkpoint files in range: [0x0000003f, 0x000041bf]
2019/04/25 12:15:41 Archive: 264 history, 263 ledger, 263 transactions, 263 results, 241 scp
2019/04/25 12:15:41 Scanning all buckets, and those referenced by range
2019/04/25 12:15:41 Archive: 2478 buckets total, 2478 referenced
2019/04/25 12:15:41 Examining checkpoint files for gaps
2019/04/25 12:15:41 Examining buckets referenced by checkpoints
2019/04/25 12:15:41 No checkpoint files missing in range [0x0000003f, 0x000041bf]
2019/04/25 12:15:41 No missing buckets referenced in range [0x0000003f, 0x000041bf]
```

Start your bantu-core instance \(`systemctl start bantu-core`\), and you should have a complete history archive being written to by your full validator.

