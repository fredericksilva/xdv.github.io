---
layout: post
title: Development Update 2
---

Production on the Divvy API began during the first week of May and is the focus for our development team over the course of the next two quarters.  The Divvy ledger has been reset to the original snapshot three times during development of the API.  At time of this writing, we are ledger 40000 and expect to reach the next level passing ledger entry 100000.  As more nodes are added, stability of the ledger will increase.  Beta testers with provable peers to the Divvy Network may receive up to 10,000 XDV per verified node by communicating with the development team on Twitter @Divvy.

Our latest snapshot was taken on ledger #40100:

{% highlight bash %}
{
   "result" : {
      "closed" : {
         "ledger" : {
            "accepted" : true,
            "account_hash" : "3641AD7AF50D2B525970CA068AB6F5B7BD16A1816DC69FD4C2311AEE9F8BE31B",
            "close_time" : 485812210,
            "close_time_human" : "2015-May-24 19:50:10",
            "close_time_resolution" : 10,
            "closed" : true,
            "fee_pool" : "1000",
            "hash" : "439ECE5E1B27B6B6BAE80FDC65D9A4E9B6751A2AE5B92F2CE6D8BD6E6446BF0A",
            "inflate_seq" : "1",
            "ledger_hash" : "439ECE5E1B27B6B6BAE80FDC65D9A4E9B6751A2AE5B92F2CE6D8BD6E6446BF0A",
            "ledger_index" : "40100",
            "parent_hash" : "7007BDA9D674382761B1FC4BFD01B7F58795098CB3ACB19E63C5D184E17049E8",
            "seqNum" : "40100",
            "totalCoins" : "99999999999999000",
            "total_coins" : "99999999999999000",
            "transaction_hash" : "0000000000000000000000000000000000000000000000000000000000000000"
         }
      },
      "open" : {
         "ledger" : {
            "closed" : false,
            "ledger_index" : "40101",
            "parent_hash" : "439ECE5E1B27B6B6BAE80FDC65D9A4E9B6751A2AE5B92F2CE6D8BD6E6446BF0A",
            "seqNum" : "40101"
         }
      },
      "status" : "success"
   }
}
{% endhighlight %}


