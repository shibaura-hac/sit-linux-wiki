# 学校のGlobalProtectにLinuxから接続する方法

２つの方法があります
- openconnect + gp-saml-gui (無料)
- Globalprotect-openconnect (有料)

## 必要なもの
- gp-saml-gui
- openconnect

## ツールのインストール

- [ ] [gp-saml-gui](https://github.com/dlenski/gp-saml-gui)
  `uv tool install https://github.com/dlenski/gp-saml-gui`
- [ ] [openconnect](https://gitlab.com/openconnect/openconnect)
  システムのパッケージマネージャーを使ってインストール


## 接続スクリプトの作成

以下の内容のスクリプトを、`~/.local/bin/connect-gp.sh` (パスが通って入ればどこでも良い) として保存し、実行権限を与える。

```shell
#!/usr/bin/env bash
set -euo pipefail

PORTAL="gpvpn.sic.shibaura-it.ac.jp"

# 1) Run SAML flow in a browser and export HOST, USER, COOKIE, OS
eval "$(gp-saml-gui --gateway "$PORTAL")"

# 2) Use the cookie with openconnect
echo "$COOKIE" | sudo -E openconnect \
  --protocol=gp \
  -u "$USER" \
  --os="$OS" \
  --usergroup="gateway:prelogin-cookie" \
  --passwd-on-stdin \
  "$HOST"
```


## 接続

connect-gp.shを実行し、認証する。管理者権限が必要。
