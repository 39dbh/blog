# copypartyをinstallして推しを眺める

### ※dockerを使います

```
mkdir copyparty
```

compose.yml

```docker
services:
  copyparty:
    image: copyparty/ac
    container_name: copyparty
    restart: unless-stopped
    user: "1000:1000"

    ports:
      - "3923:3923"

    volumes:
      - ./cfg:/cfg
      - /srv/up/:/srv/up:rw
      - /srv/images:/srv/images:ro
```

```
mkdir -p ./cfg/hists/
```

```
sudo nano copyparty.conf
```

```YAML
[global]
  hist: /cfg/hists/
  e2ts, e2dsa

[accounts]
  user: password

[/up]
  /srv/up
  accs:
    rwmd: user

[/images]
  /srv/images
  accs:
    r: user
```
#### 解説として

`/cfg/hists/`これは`volumes`で指定したディレクトリを扱うので`mkdir -p ./cfg/hists/`を実行しることを忘れないようにしておきましょう

`user: password`でパスワードをゴニョゴニョしてくださいね

`[/up]`ここは表示名

`/srv/up`使用するディレクトリ

`: user`使用するユーザを指定する

`rwmd`書き込み許可

逆に`r:`は読み込みのみってことですね

---

### Nginx Prxy Manager

とは言っても`Websockets Support`をONにすればいいだけなので

---

割とあっさりとできるのが利点で良いですね

ProxmoxのLXCコンテナで運用してますがリソースは食わないのでLXCで良さそうですね