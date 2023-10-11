### openwrt support status

|   Version    |  status   |                     link                      |
| :----------: | :-------: | :-------------------------------------------: |
| openwrt main | supported | https://github.com/openwrt/openwrt/pull/13414 |

### compile

```
# Clone the official warehouse of openwrt
git clone https://github.com/openwrt/openwrt.git && cd openwrt

# Update the feeds
./scripts/feeds update -a
./scripts/feeds install -a

# Configure the firmware image
cat > .config << EOF
CONFIG_TARGET_mediatek=y
CONFIG_TARGET_mediatek_filogic=y
CONFIG_TARGET_mediatek_filogic_DEVICE_glinet_gl-mt6000=y
EOF

# Build the firmware image
make defconfig
make
```
