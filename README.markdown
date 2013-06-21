libunbound for Prosody

This file replaces Prosodys internal DNS library with a LuaJIT FFI binding to
libunbound.  It was mostly created as an experiment to see if it was possible,
and to play with LuaJIT and its FFI.  Note that you need LuaJIT 2 (beta10 is
the latest as of this writing).

With version 2, lib.unbound.lua should work as a standalone library.  Note that
you still need to parse the RR data yourself.

See
* http://prosody.im/
* http://luajit.org/
* https://unbound.net/

How to build:
`./squish.sh > use_unbound.lua`

How to install:
1. Put use_unbound.lua in /etc/prosody or where your prosody.cfg.lua lives.
2. In the global section of your prosody.cfg.lua, add the following:

RunScript "use_unbound.lua"
resolvconf = "/etc/resolv.conf"
hoststxt = "/etc/hosts"

3. Then start Prosody in LuaJIT. (How to do this is left as an exercise.)
4. If you have debug logging enabled, you should see logs from 'unbound' about
	lookups performed.

Configuration:
* resolvconf - string, filename
Optional, but recommended. Point to a file with a list of name servers to use.
If left out, unbound will perform a full lookup from scratch from the DNS roots.

* hoststxt - string, filename
Optional. Point to a file like /etc/hosts or similar. Note that XMPP servers use
SRV lookups first to know where to connect to.