```bash
# list
git config --global --list
```

```bash
# set
git config --global user.name 'xxxxx'
git config --global user.email 'xxxxx@xx.com'
```

proxy:
```bash
# set proxy
git config --global http.proxy http://127.0.0.1:1080
git config --global https.proxy http://127.0.0.1:1080

# delete proxy
git config --global --unset http.proxy
git config --global --unset https.proxy
```