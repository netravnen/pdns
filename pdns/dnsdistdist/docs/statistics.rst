Statistics
==========

dnsdist keeps statistics on the queries is receives and send out. They can be accessed in different ways:

- via the console (see :ref:`Console`), using :func:`dumpStats` for the general ones,
  :func:`showServers()` for the ones related to the backends, :func:`showBinds()` for the frontends,
  `getPool("pool name"):getCache():printStats()` for the ones related to a specific cache and so on
- via the internal webserver (see :doc:`../guides/webserver`) which includes a Prometheus endpoint
- via Carbon / Graphite / Metronome export (see :doc:`../guides/carbon`)
- via SNMP (see :doc:`../advanced/snmp`)

To make sense of the statistics, the following relation should hold:

	queries - noncompliant-queries
	=
	responses - noncompliant-responses + cache-hits + downstream-timeouts + self-answered + no-policy
	+ rule-drop

Note that packets dropped by eBPF (see :doc:`../advanced/ebpf`) are
accounted for in the eBPF statistics, and do not show up in the metrics
described on this page.

acl-drops
---------
The number of packets (or TCP messages) dropped because of the :doc:`ACL <advanced/acl>`.
If a packet or message is dropped, it is not counted in the `queries` statistic.

cache-hits
----------
Number of times a response was sent using data found in the :doc:`packet cache <guides/cache>`.

cache-misses
------------
Number of times an answer was not found in the :doc:`packet cache <guides/cache>`. Only counted if a packet cache was setup for the selected pool.

cpu-iowait
----------
.. versionadded:: 1.5.0

Time spent waiting for I/O to complete by the whole system, in units of USER_HZ.

cpu-steal
---------
.. versionadded:: 1.5.0

Stolen time, which is the time spent by the whole system in other operating systems when running in a virtualized environment, in units of USER_HZ.

cpu-sys-msec
------------
Milliseconds spent by :program:`dnsdist` in the "system" state.

cpu-user-msec
-------------
Milliseconds spent by :program:`dnsdist` in the "user" state.

doh-query-pipe-full
-------------------
Number of queries dropped because the internal DoH pipe was full.

doh-response-pipe-full
----------------------
Number of responses dropped because the internal DoH pipe was full.

downstream-send-errors
----------------------
Number of errors when sending a query to a backend.

downstream-timeouts
-------------------
Number of queries not answer in time by a backend.

dyn-block-nmg-size
------------------
Number of dynamic blocks entries.

dyn-blocked
-----------
Number of queries dropped because of a dynamic block.

empty-queries
-------------
Number of empty queries received from clients. Every empty-query is also
counted as a `query`.

fd-usage
--------
Number of currently used file descriptors.

frontend-noerror
----------------
Number of NoError answers sent to clients.

frontend-nxdomain
-----------------
Number of NXDomain answers sent to clients.

frontend-servfail
-----------------
Number of ServFail answers sent to clients.

latency-avg100
--------------
Average response latency in microseconds of the last 100 packets

latency-avg1000
---------------
Average response latency in microseconds of the last 1000 packets.

latency-avg10000
----------------
Average response latency in microseconds of the last 10000 packets.

latency-avg1000000
------------------
Average response latency in microseconds of the last 1000000 packets.

latency-bucket
--------------
Histogram of response time latencies.

latency-count
-------------
Number of queries contributing to response time histogram and latency sum.

latency-doh-avg100
------------------
Average response latency, in microseconds, of the last 100 packets received over DoH.

latency-doh-avg1000
-------------------
Average response latency, in microseconds, of the last 1000 packets received over DoH.

latency-doh-avg10000
--------------------
Average response latency, in microseconds, of the last 10000 packets received over DoH.

latency-doh-avg100000
---------------------
Average response latency, in microseconds, of the last 100000 packets received over DoH.

latency-dot-avg100
------------------
Average response latency, in microseconds, of the last 100 packets received over DoT.

latency-dot-avg1000
-------------------
Average response latency, in microseconds, of the last 1000 packets received over DoT.

latency-dot-avg10000
--------------------
Average response latency, in microseconds, of the last 10000 packets received over DoT.

latency-dot-avg1000000
----------------------
Average response latency, in microseconds, of the last 1000000 packets received over DoT.

latency-slow
------------
Number of queries answered in more than 1 second.

latency-sum
-----------
Total response time of all queries combined in milliseconds since the start of dnsdist. Can be used to calculate the
average response time over all queries.

latency-tcp-avg100
------------------
Average response latency, in microseconds, of the last 100 packets received over TCP.

latency-tcp-avg1000
-------------------
Average response latency, in microseconds, of the last 1000 packets received over TCP.

latency-tcp-avg10000
--------------------
Average response latency, in microseconds, of the last 10000 packets received over TCP.

latency-tcp-avg1000000
----------------------
Average response latency, in microseconds, of the last 1000000 packets received over TCP.

latency0-1
----------
Number of queries answered in less than 1 ms.

latency1-10
-----------
Number of queries answered in 1-10 ms.

latency10-50
------------
Number of queries answered in 10-50 ms.

latency50-100
-------------
Number of queries answered in 50-100 ms.

latency100-1000
---------------
Number of queries answered in 100-1000 ms.

no-policy
---------
Number of queries dropped because no server was available.

noncompliant-queries
--------------------
Number of queries dropped as non-compliant.

noncompliant-responses
----------------------
Number of answers from a backend dropped as non-compliant.

outgoing-doh-query-pipe-full
----------------------------
Number of outgoing DoH queries dropped because the internal pipe used to distribute queries was full.

proxy-protocol-invalid
----------------------
.. versionadded:: 1.6.0

Number of queries dropped because of an invalid Proxy Protocol header.

queries
-------
Number of received queries.

rdqueries
---------
Number of received queries with the recursion desired bit set.

real-memory-usage
-----------------
Current memory usage.

responses
---------
Number of responses received from backends. Note! This is not the number of
responses sent to clients. To get that number, add 'cache-hits' and
'responses'.

rule-drop
---------
Number of queries dropped because of a rule.

rule-nxdomain
-------------
Number of NXDomain answers returned because of a rule.

rule-refused
------------
Number of Refused answers returned because of a rule.

rule-servfail
-------------
Number of ServFail answers returned because of a rule.

rule-truncated
--------------
.. versionadded:: 1.6.0

Number of truncated answers returned because of a rule.

security-status
---------------
The security status of :program:`dnsdist`. This is regularly polled.

 * 0 = Unknown status or unreleased version
 * 1 = OK
 * 2 = Upgrade recommended
 * 3 = Upgrade required (most likely because there is a known security issue)

self-answered
-------------
Number of self-answered responses.

servfail-responses
------------------
Number of servfail answers received from backends.

tcp-cross-protocol-query-pipe-full
----------------------------------
Number of TCP cross-protocol queries dropped because the internal pipe used to distribute queries was full.

tcp-cross-protocol-response-pipe-full
-------------------------------------
Number of TCP cross-protocol responses dropped because the internal pipe used to distribute queries was full.

tcp-listen-overflows
--------------------
.. versionadded:: 1.6.0

From /proc/net/netstat ListenOverflows.

tcp-query-pipe-full
-------------------
Number of TCP queries dropped because the internal pipe used to distribute queries was full.

trunc-failures
--------------
Number of errors encountered while truncating an answer.

udp-in-csum-errors
------------------
.. versionadded:: 1.7.0

From /proc/net/snmp InErrors.

udp-in-errors
-------------
.. versionadded:: 1.5.0

From /proc/net/snmp InErrors.

udp-noport-errors
-----------------
.. versionadded:: 1.5.0

From /proc/net/snmp NoPorts.

udp-recvbuf-errors
------------------
.. versionadded:: 1.5.0

From /proc/net/snmp RcvbufErrors.

udp-sndbuf-errors
-----------------
.. versionadded:: 1.5.0

From /proc/net/snmp SndbufErrors.

udp6-in-csum-errors
-------------------
.. versionadded:: 1.7.0

From /proc/net/snmp6 InErrors.

udp6-in-errors
--------------
.. versionadded:: 1.7.0

From /proc/net/snmp6 InErrors.

udp6-noport-errors
------------------
.. versionadded:: 1.7.0

From /proc/net/snmp6 NoPorts.

udp6-recvbuf-errors
-------------------
.. versionadded:: 1.7.0

From /proc/net/snmp6 RcvbufErrors.

udp6-sndbuf-errors
------------------
.. versionadded:: 1.7.0

From /proc/net/snmp6 SndbufErrors.

uptime
------
Uptime of the dnsdist process, in seconds.
