# aliyundrive-fuse

[![GitHub Actions](https://github.com/messense/aliyundrive-fuse/workflows/CI/badge.svg)](https://github.com/messense/aliyundrive-fuse/actions?query=workflow%3ACI)
[![PyPI](https://img.shields.io/pypi/v/aliyundrive-fuse.svg)](https://pypi.org/project/aliyundrive-fuse)
[![Docker Image](https://img.shields.io/docker/pulls/messense/aliyundrive-fuse.svg?maxAge=2592000)](https://hub.docker.com/r/messense/aliyundrive-fuse/)
[![aliyundrive-fuse](https://snapcraft.io/aliyundrive-fuse/badge.svg)](https://snapcraft.io/aliyundrive-fuse)
[![Crates.io](https://img.shields.io/crates/v/aliyundrive-fuse.svg)](https://crates.io/crates/aliyundrive-fuse)

> ð Help me to become a full-time open-source developer by [sponsoring me on GitHub](https://github.com/sponsors/messense)

é¿éäºç FUSE ç£çæè½½ï¼ä¸»è¦ç¨äºéå [Emby](https://emby.media) æè [Jellyfin](https://jellyfin.org) è§çé¿éäºçåå®¹ï¼åè½ç¹æ§ï¼

1. ç®ååªè¯»ï¼ä¸æ¯æåå¥
2. æ¯æ Linux å macOSï¼æä¸æ¯æ Windows

[aliyundrive-webdav](https://github.com/messense/aliyundrive-webdav) é¡¹ç®å·²ç»å®ç°äºéè¿ WebDAV è®¿é®é¿éäºçåå®¹ï¼ä½ç±äº Emby å Jellyfin é½ä¸æ¯æç´æ¥è®¿é® WebDAV èµæºï¼
éè¦éå [rclone](https://rclone.org) ä¹ç±»çè½¯ä»¶å° WebDAV æè½½ä¸ºæ¬å°ç£çï¼èæ¬é¡¹ç®åç´æ¥éè¿ FUSE å®ç°å°é¿éäºçæè½½ä¸ºæ¬å°ç£çï¼çå»ä½¿ç¨ rclone ååä¸å±ä¸­è½¬ã

## å®è£

* macOS éè¦åå®è£ [macfuse](https://osxfuse.github.io/)
* Linux éè¦åå®è£ fuse
  * Debian ç³»å¦ Ubuntu: `apt-get install -y fuse3`
  * RedHat ç³»å¦ CentOS: `yum install -y fuse3`

å¯ä»¥ä» [GitHub Releases](https://github.com/messense/aliyundrive-fuse/releases) é¡µé¢ä¸è½½é¢åæå»ºçäºè¿å¶åï¼ ä¹å¯ä»¥ä½¿ç¨ pip ä» PyPI ä¸è½½:

```bash
pip install aliyundrive-fuse
```

å¦æç³»ç»æ¯æ [Snapcraft](https://snapcraft.io) æ¯å¦ UbuntuãDebian ç­ï¼ä¹å¯ä»¥ä½¿ç¨ snap å®è£ï¼

```bash
sudo snap install aliyundrive-fuse
```

### OpenWrt è·¯ç±å¨

[GitHub Releases](https://github.com/messense/aliyundrive-fuse/releases) ä¸­æé¢ç¼è¯ç ipk æä»¶ï¼ ç®åæä¾äº
aarch64/arm/x86_64/i686 ç­æ¶æççæ¬ï¼å¯ä»¥ä¸è½½åä½¿ç¨ opkg å®è£ï¼ä»¥ nanopi r4s ä¸ºä¾ï¼

```bash
wget https://github.com/messense/aliyundrive-fuse/releases/download/v0.1.14/aliyundrive-fuse_0.1.14-1_aarch64_generic.ipk
wget https://github.com/messense/aliyundrive-fuse/releases/download/v0.1.14/luci-app-aliyundrive-fuse_0.1.14_all.ipk
wget https://github.com/messense/aliyundrive-fuse/releases/download/v0.1.14/luci-i18n-aliyundrive-fuse-zh-cn_0.1.14-1_all.ipk
opkg install aliyundrive-fuse_0.1.14-1_aarch64_generic.ipk
opkg install luci-app-aliyundrive-fuse_0.1.14_all.ipk
opkg install luci-i18n-aliyundrive-fuse-zh-cn_0.1.14-1_all.ipk
```

å¶å® CPU æ¶æçè·¯ç±å¨å¯å¨ [GitHub Releases](https://github.com/messense/aliyundrive-fuse/releases) é¡µé¢ä¸­æ¥æ¾å¯¹åºçæ¶æçä¸»ç¨åº ipk æä»¶ä¸è½½å®è£ã

> Tips: ä¸æ¸æ¥ CPU æ¶æç±»åå¯éè¿è¿è¡ `opkg print-architecture` å½ä»¤æ¥è¯¢ã

## å½ä»¤è¡ç¨æ³

```bash
USAGE:
    aliyundrive-fuse [OPTIONS] --refresh-token <REFRESH_TOKEN> <PATH>

ARGS:
    <PATH>    Mount point

OPTIONS:
        --allow-other                            Allow other users to access the drive
        --domain-id <DOMAIN_ID>                  Aliyun PDS domain id
    -h, --help                                   Print help information
    -r, --refresh-token <REFRESH_TOKEN>          Aliyun drive refresh token [env: REFRESH_TOKEN=]
    -S, --read-buffer-size <READ_BUFFER_SIZE>    Read/download buffer size in bytes, defaults to 10MB [default: 10485760]
    -V, --version                                Print version information
    -w, --workdir <WORKDIR>                      Working directory, refresh_token will be stored in there if specified
```

æ¯å¦å°ç£çæè½½å° `/mnt/aliyundrive` ç®å½ï¼

```bash
mkdir -p /mnt/aliyundrive /var/run/aliyundrive-fuse
aliyundrive-fuse -r your-refresh-token -w /var/run/aliyundrive-fuse /mnt/aliyundrive
```

## Emby/Jellyfin

å¦ææ¯ç´æ¥è¿è¡å¨ç³»ç»ä¸ç Emby/Jellyfinï¼åå¯ä»¥ç´æ¥å¨å¶æ§å¶å°æ·»å åªä½åºçæ¶åéæ©é¿éäºçå¯¹åºçæè½½è·¯å¾ä¸­çæä»¶å¤¹å³å¯ï¼
å¦ææ¯ Docker è¿è¡ç Emby/Jellyfinï¼åéè¦å°é¿éäºçæè½½è·¯å¾ä¹æè½½å° Docker å®¹å¨ä¸­ï¼åè®¾é¿éäºçæè½½è·¯å¾ä¸º `/mnt/aliyundrive`ï¼
ä»¥ Jellyfin ä¸ºä¾ï¼åè®¾ Jellyfin å·¥ä½è·¯å¾ä¸º `/root/jellyfin`ï¼å°äºçæè½½å°å®¹å¨ `/media` è·¯å¾ï¼

```bash
docker run -d --name jellyfin \
  -v /root/jellyfin/config:/config \
  -v /root/jellyfin/cache:/cache \
  -v /mnt/aliyundrive:/media \
  -p 8096:8096 \
  --device=/dev/dri/renderD128 \
  --device /dev/dri/card0:/dev/dri/card0 \
  --restart unless-stopped \
  jellyfin/jellyfin
```

## License

This work is released under the MIT license. A copy of the license is provided in the [LICENSE](./LICENSE) file.
