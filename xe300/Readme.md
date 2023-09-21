### openwrt support status

| Version       | status    | link                                                  |
| ------------- | --------- | ----------------------------------------------------- |
| openwrt 19.07 | supported | https://github.com/openwrt/openwrt/tree/openwrt-19.07 |
| openwrt 21.02 | supported |                                                       |
| openwrt 22.04 | supported |                                                       |
| openwrt 23.05 | supported |                                                       |

### compile

```
git clone https://github.com/openwrt/openwrt.git && cd openwrt
cat > .config << EOF
CONFIG_TARGET_ath79=y
CONFIG_TARGET_ath79_nand=y
CONFIG_TARGET_ath79_nand_DEVICE_glinet_gl-xe300-nor-nand=y
EOF
make defconfig
make
```

