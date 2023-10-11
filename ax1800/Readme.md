### openwrt support status

| Version      | status       | link                                                         |
| :----------: | :----------: | :----------------------------------------------------------: |
| wlan-ap v2.11.0 | supported | https://github.com/Telecominfraproject/wlan-ap/tree/v2.11.0 |
| wlan-ap v2.10.0 | supported | https://github.com/Telecominfraproject/wlan-ap/tree/v2.10.0 |
| wlan-ap v2.9.0 | supported | https://github.com/Telecominfraproject/wlan-ap/tree/v2.9.0 |
| wlan-ap v2.8.0 | supported | https://github.com/Telecominfraproject/wlan-ap/tree/v2.8.0 |
| wlan-ap v2.7.0 | supported | https://github.com/Telecominfraproject/wlan-ap/tree/v2.7.0 |
| wlan-ap v2.6.0 | supported | https://github.com/Telecominfraproject/wlan-ap/tree/v2.6.0 |
| wlan-ap v2.5.0 | supported | https://github.com/Telecominfraproject/wlan-ap/tree/v2.5.0 |

### compile

```
# Setting up your build machine
https://openwrt.org/docs/guide-developer/toolchain/beginners-build-guide

# Clone the official warehouse of openwrt
git clone https://github.com/Telecominfraproject/wlan-ap.git && cd wlan-ap

# Select a specific code revision
git checkout v2.11.0

# Clone and set up the tree
./setup.py --setup && cd openwrt
./scripts/gen_config.py ../profiles/glinet_ax1800.yml

# Configure the firmware image
cat >> .config << EOF
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

# Change the dependency of firewall
sed -i 's/+uci-firewall/+firewall/g' ./package/feeds/luci/luci-app-firewall/Makefile

# Delete root password
# File path : wlan-ap/openwrt/package/base-files/files/etc/shadow

# Build the firmware image
make defconfig
make V=s -j1
# Image path : wlan-ap/openwrt/bin/targets/ipq807x/ipq60xx/openwrt-ipq807x-glinet_ax1800-squashfs-sysupgrade.tar
# Warning : the image needs to be upgraded in the system management interface.
```
