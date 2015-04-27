---
layout: post
title: Development Update #1
---

Payshares is now forging consensus and the initial reference implementation of XPR is available at https://github.com/payshares/paysharesd

Support is being provided for Ubuntu 14.04 LTS 64-bit.  It is recommended to have at least 2 GB RAM, a quad core processor, and adequate disk space.  Installation of paysharesd on Ubuntu 14.04 is relatively straightforward with administrator privileges:

{% highlight bash %}
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install git autoconf autogen automake build-essential software-properties-common libboost-all-dev libcurl4-openssl-dev libdb-dev libdb++-dev libgmp3-dev libminiupnpc-dev libmpfr-dev libssl-dev libcurl4-openssl-dev libjansson-dev pax-utils
sudo apt-get install git scons ctags pkg-config protobuf-compiler libprotobuf-dev libssl-dev python-software-properties libboost1.55-all-dev g++ make
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.8 40 --slave /usr/bin/g++ g++ /usr/bin/g++-4.8
sudo update-alternatives --config gcc
wget https://download.libsodium.org/libsodium/releases/LATEST.tar.gz
tar xzf LATEST.tar.gz
cd libsodium-0.6.1/
./configure
make && make check && sudo make install
cd ..
git clone https://github.com/payshares/paysharesd.git
cd paysharesd/
scons
{% endhighlight %}

After compilation, paysharesd will be available within the 'build' directory.  paysharesd.cfg should be placed in the ~/.config/payshares directory.  Create the following directories:

{% highlight bash %}
(if not exists):
mkdir ~/.config

mkdir ~/.config/payshares
mkdir ~/.config/payshares/db
{% endhighlight %}

The published documentation will be updated to reflect the initial validating node as referenced in the following example paysharesd.cfg:

{% highlight bash %}
# Allow other peers to connect to this server.
#
[peer_ip]
0.0.0.0

[peer_port]
52011

# Allow untrusted clients to connect to this server.
#
[websocket_public_ip]
0.0.0.0

[websocket_public_port]
5016

# Provide trusted websocket ADMIN access to the localhost.
#
[websocket_ip]
127.0.0.1

[websocket_port]
6016

# Provide trusted json-rpc ADMIN access to the localhost.
#
[rpc_ip]
127.0.0.1

[rpc_port]
5015

[rpc_allow_remote]
0

[node_size]
medium

# This is primary persistent datastore for paysharesd.  This includes transaction
# metadata, account states, and ledger headers.  
[node_db]
type=RocksDB
path=<userpath>/.config/payshares/db/rocksdb
open_files=2000
filter_bits=12
cache_mb=256
file_size_mb=8
file_size_mult=2

[database_path]
<userpath>/.config/payshares/db

# This needs to be an absolute directory reference, not a relative one.
# Modify this value as required.
[debug_logfile]
<userpath>/.config/payshares/debug.log

[sntp_servers]
time.windows.com
time.apple.com
time.nist.gov
pool.ntp.org

# Where to find some other servers speaking the Payshares protocol.
#
[ips]
one.validator.payshares.co 52011

[validators]
naKF9vP6PmUDudBVkXHfr3cRScQideaMsFa9crvntk7x9VYPUTr SDF1

# Ditto.
[validation_quorum]
1

[consensus_threshold]
-1

# Turn down default logging to save disk space in the long run.
# Valid values here are trace, debug, info, warning, error, and fatal
[rpc_startup]
{ "command": "log_level", "severity": "warning" }

# Configure SSL for WebSockets.  Not enabled by default because not everybody
# has an SSL cert on their server, but if you uncomment the following lines and
# set the path to the SSL certificate and private key the WebSockets protocol
# will be protected by SSL/TLS.
#[websocket_secure]
#1

#[websocket_ssl_cert]
#/etc/ssl/certs/server.crt

#[websocket_ssl_key]
#/etc/ssl/private/server.key

# Defaults to 0 ("no") so that you can use self-signed SSL certificates for
# development, or internally.
#[ssl_verify]
#0
{% endhighlight %}

Our latest snapshot was taken on ledger #2271:

{% highlight bash %}
{
   "result" : {
      "closed" : {
         "ledger" : {
            "accepted" : true,
            "account_hash" : "3132824E4160B0A93FCA8637AEA85F542EB7D6F40EC85E0F78E05DB3CC77285A",
            "close_time" : 483487240,
            "close_time_human" : "2015-Apr-27 22:00:40",
            "close_time_resolution" : 10,
            "closed" : true,
            "fee_pool" : "1000",
            "hash" : "3B4D4D27C8582E012857DBB14A152F2B775BCD1D328C413283BBEF92DCF0C55B",
            "inflate_seq" : "1",
            "ledger_hash" : "3B4D4D27C8582E012857DBB14A152F2B775BCD1D328C413283BBEF92DCF0C55B",
            "ledger_index" : "2271",
            "parent_hash" : "48C16D6614AF91901CEA09121A8F0B621BFD055A85F01B8254C4A973A868D42C",
            "seqNum" : "2271",
            "totalCoins" : "99999999999999000",
            "total_coins" : "99999999999999000",
            "transaction_hash" : "0000000000000000000000000000000000000000000000000000000000000000"
         }
      },
      "open" : {
         "ledger" : {
            "closed" : false,
            "ledger_index" : "2272",
            "parent_hash" : "3B4D4D27C8582E012857DBB14A152F2B775BCD1D328C413283BBEF92DCF0C55B",
            "seqNum" : "2272"
         }
      },
      "status" : "success"
   }
}
{% endhighlight %}


