warning: LF will be replaced by CRLF in test.md. (Whitespace 에러)

for windowns
```bash
git config --global core.autocrlf true
```

for linux or mac
```bash
git config --global core.autocrlf true input
```

변환 기능을 원하지 않고, 그냥 에러 메시지 끄고 알아서 작업하고 싶은 경우
```bash
git config --global core.safecrlf false
```

REF. https://blog.jaeyoon.io/2018/01/git-crlf.html
