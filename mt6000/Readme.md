### openwrt support status

| Version      | status       | link                                                         |
| ------------ | ------------ | ------------------------------------------------------------ |
| openwrt main | under review | https://github.com/openwrt/openwrt/pull/13414/commits/f088f39856b2c0b991f42a9d62ddc822a72de297 |
|              |              |                                                              |
|              |              |                                                              |
|              |              |                                                              |

### compile

```
# Clone the official warehouse of openwrt
git clone https://github.com/openwrt/openwrt.git && cd openwrt

# Select a specific code revision
git checkout openwrt-23.05

# Update the feeds
./scripts/feeds update -a
./scripts/feeds install -a

# Configure the firmware image
cat > .config << EOF
CONFIG_TARGET_ath79=y
CONFIG_TARGET_ath79_nand=y
CONFIG_TARGET_ath79_nand_DEVICE_glinet_gl-xe300-nor-nand=y
EOF

# Build the firmware image
make defconfig
make
```
