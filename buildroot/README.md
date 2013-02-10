Tvheadend buildroot config
==========================

1. Copy package/tvheadend/ to your buildroot
2. Add "source "package/tvheadend/Config.in"" to package/Config.in, before
   the udpcast entry.
3. Ensure that the following options are enabled in buildroot config:
  - Toolchain > Enable large file
  - Toolchain > Enable IPV6 support
  - Package > Networking applications > Tvheadend
4. Optionally you can enable:
  - imagecache : Package > Libraries > Networking > libcurl
  - avahi : Package > Networking applications > avahi
  - zlib: Package > Libraries > Compression > zlib

5. If you're rebuilding you may need to remove all of:
  - dl/tvheadend*
  - output/build/tvheadend*

TBS MOI
-------

For compiling for the TBS MOI you need to configure buildroot as follows:

- Target Architecture > ARM (little endian)
- Target Architecture Variant > cortex-A8
- Target ABI > EABI

Once compiled you can simply copy the binary and init scripts to the box

- build/target/usr/bin/tvheadend -> MOI:/usr/bin/tvheadend
- build/target/etc/default/tvheadend -> MOI:/etc/default/tvheadend
- build/target/etc/init.d/S99tvheadend -> MOI:/etc/init.d/S99tvheadend
- build/target/root/.hts/tvheadend/accesscontrol/1 MOI:/root/.hts/tvheadend/accesscontrol/1
- build/target/usr/lib/ MOI:/usr/lib

Note: if installing onto a pre-configured MOI image you probably have to
remove /etc/init.d/S99tv

Note: The last step (accesscontrol) only needs to be done once

Note: timeshift is currently disabled

Note: dvbcsa is still not linked, so descrambling might be an issue

Note: you probably need to set TVH_DELAY=10 to ensure good startup

Note: you may need to set TVH_USER/GROUP = root, due to default
      adapter permissions
