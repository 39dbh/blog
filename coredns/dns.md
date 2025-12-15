# coreDNSのinstall

go言語とmake&gitをinstall

```
sudo apt update
sudo apt install -y make golang-go git
```

```
git clone https://github.com/coredns/coredns
cd coredns
make
```
```
sudo nano Corefile
```
```
# ===== .arai (local-only) =====
arai {
    # *.arai をすべて Reverse Proxy (VIP) に向ける
    template IN A {
        match (.*)\.arai
        answer "{{ .Name }} 60 IN A 192.168.3.100"
    }

    # 念のため NS/SOA を返す
    ns .
    log
    errors
}

# ===== その他は上流DNSへ =====
. {
    forward . 1.1.1.1 8.8.8.8
    cache 300
    log
    errors
}

```