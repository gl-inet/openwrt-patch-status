### openwrt support status

| Version      | status       | link                                                         |
| :----------: | :----------: | :----------------------------------------------------------: |
| openwrt 23.05 | supported | https://github.com/openwrt/openwrt/tree/openwrt-23.05 |
| openwrt 22.03 | supported | https://github.com/openwrt/openwrt/tree/openwrt-22.03 |

### compile

```
# Setting up your build machine
https://openwrt.org/docs/guide-developer/toolchain/beginners-build-guide

# Clone the official warehouse of openwrt
git clone https://github.com/openwrt/openwrt.git && cd openwrt

# Select a specific code revision
git checkout v23.05.0-rc4

# Update the feeds
./scripts/feeds update -a
./scripts/feeds install -a

# Configure the firmware image
cat > .config << EOF
CONFIG_TARGET_ath79=y
CONFIG_TARGET_ath79_generic=y
CONFIG_TARGET_ath79_generic_DEVICE_glinet_gl-x300b=y
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

# Build the firmware image
make defconfig
make V=s -j1

# Image path : openwrt/bin/targets/ath79/generic/openwrt-ath79-generic-glinet_gl-x300b-squashfs-sysupgrade.bin
```
