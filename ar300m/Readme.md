### openwrt support status

| Version      | status       | link                                                         |
| ------------ | ------------ | ------------------------------------------------------------ |
| openwrt main | supported | https://github.com/openwrt/openwrt/tree/openwrt-23.05 |
|              |              |                                                              |
|              |              |                                                              |
|              |              |                                                              |

### compile

```
#Setting up your build machine
https://openwrt.org/docs/guide-developer/toolchain/beginners-build-guide

# Clone the official warehouse of openwrt
git clone https://github.com/openwrt/openwrt.git && cd openwrt

# Select a specific code revision
git checkout v23.05.0-rc4

# Update the feeds
./scripts/feeds update -a
./scripts/feeds install -a

# Configure the firmware image
# start from nand flash
cat > .config << EOF
CONFIG_TARGET_ath79=y
CONFIG_TARGET_ath79_generic=y
CONFIG_TARGET_ath79_nand_DEVICE_glinet_gl-ar300m16-nand=y
CONFIG_PACKAGE_cgi-io=y
CONFIG_PACKAGE_liblua=y
CONFIG_PACKAGE_liblucihttp=y
CONFIG_PACKAGE_liblucihttp-lua=y
CONFIG_PACKAGE_liblucihttp-ucode=y
CONFIG_PACKAGE_libubus-lua=y
CONFIG_PACKAGE_lua=y
CONFIG_PACKAGE_luci=y
CONFIG_PACKAGE_luci-app-firewall=y
CONFIG_PACKAGE_luci-app-opkg=y
CONFIG_PACKAGE_luci-base=y
CONFIG_PACKAGE_luci-compat=y
CONFIG_PACKAGE_luci-lib-base=y
CONFIG_PACKAGE_luci-lib-ip=y
CONFIG_PACKAGE_luci-lib-json=y
CONFIG_PACKAGE_luci-lib-jsonc=y
CONFIG_PACKAGE_luci-lib-nixio=y
CONFIG_PACKAGE_luci-light=y
CONFIG_PACKAGE_luci-lua-runtime=y
CONFIG_PACKAGE_luci-mod-admin-full=y
CONFIG_PACKAGE_luci-mod-network=y
CONFIG_PACKAGE_luci-mod-rpc=y
CONFIG_PACKAGE_luci-mod-status=y
CONFIG_PACKAGE_luci-mod-system=y
CONFIG_PACKAGE_luci-proto-ipv6=y
CONFIG_PACKAGE_luci-proto-ppp=y
CONFIG_PACKAGE_luci-theme-bootstrap=y
CONFIG_PACKAGE_rpcd=y
CONFIG_PACKAGE_rpcd-mod-file=y
CONFIG_PACKAGE_rpcd-mod-iwinfo=y
CONFIG_PACKAGE_rpcd-mod-luci=y
CONFIG_PACKAGE_rpcd-mod-rrdns=y
CONFIG_PACKAGE_rpcd-mod-ucode=y
CONFIG_PACKAGE_ucode-mod-html=y
CONFIG_PACKAGE_ucode-mod-lua=y
CONFIG_PACKAGE_ucode-mod-math=y
CONFIG_PACKAGE_uhttpd=y
CONFIG_PACKAGE_uhttpd-mod-ubus=y
EOF

# start from nor flash
cat > .config << EOF
 29 CONFIG_TARGET_ath79=y
 30 CONFIG_TARGET_ath79_generic=y
 31 CONFIG_TARGET_ath79_nand_DEVICE_glinet_gl-ar300m-nor=y
 32 CONFIG_PACKAGE_cgi-io=y
 33 CONFIG_PACKAGE_liblua=y
 34 CONFIG_PACKAGE_liblucihttp=y
 35 CONFIG_PACKAGE_liblucihttp-lua=y
 36 CONFIG_PACKAGE_liblucihttp-ucode=y
 37 CONFIG_PACKAGE_libubus-lua=y
 38 CONFIG_PACKAGE_lua=y
 39 CONFIG_PACKAGE_luci=y
 40 CONFIG_PACKAGE_luci-app-firewall=y
 41 CONFIG_PACKAGE_luci-app-opkg=y
 42 CONFIG_PACKAGE_luci-base=y
 43 CONFIG_PACKAGE_luci-compat=y
 44 CONFIG_PACKAGE_luci-lib-base=y
 45 CONFIG_PACKAGE_luci-lib-ip=y
 46 CONFIG_PACKAGE_luci-lib-json=y
 47 CONFIG_PACKAGE_luci-lib-jsonc=y
 48 CONFIG_PACKAGE_luci-lib-nixio=y
 49 CONFIG_PACKAGE_luci-light=y
 50 CONFIG_PACKAGE_luci-lua-runtime=y
 51 CONFIG_PACKAGE_luci-mod-admin-full=y
 52 CONFIG_PACKAGE_luci-mod-network=y
 53 CONFIG_PACKAGE_luci-mod-rpc=y
 54 CONFIG_PACKAGE_luci-mod-status=y
 55 CONFIG_PACKAGE_luci-mod-system=y
 56 CONFIG_PACKAGE_luci-proto-ipv6=y
 57 CONFIG_PACKAGE_luci-proto-ppp=y
 58 CONFIG_PACKAGE_luci-theme-bootstrap=y
 59 CONFIG_PACKAGE_rpcd=y
 60 CONFIG_PACKAGE_rpcd-mod-file=y
 61 CONFIG_PACKAGE_rpcd-mod-iwinfo=y
 62 CONFIG_PACKAGE_rpcd-mod-luci=y
 63 CONFIG_PACKAGE_rpcd-mod-rrdns=y
 64 CONFIG_PACKAGE_rpcd-mod-ucode=y
 65 CONFIG_PACKAGE_ucode-mod-html=y
 66 CONFIG_PACKAGE_ucode-mod-lua=y
 67 CONFIG_PACKAGE_ucode-mod-math=y
 68 CONFIG_PACKAGE_uhttpd=y
 69 CONFIG_PACKAGE_uhttpd-mod-ubus=y
 70 EOF

# Build the firmware image
make defconfig
make V=s -j1

# nand image path : openwrt/bin/targets/ath79/nand/openwrt-ath79-generic-glinet_gl-ar300m-nand-squashfs-sysupgrade.bin
# nor image path : openwrt/bin/targets/ath79/nand/openwrt-ath79-generic-glinet_gl-ar300m-nor-squashfs-sysupgrade.bin
```