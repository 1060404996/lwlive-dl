# LwLive 下载中转仓库

本仓库用于 **LwLive App 下载地址中转**，隐藏真实下载域名（img.yjtv.top），让用户看到的下载链接只显示 github.io。

## 下载链路

```
落地页 / App 按钮 → https://1060404996.github.io/lwlive-dl/go/ios | go/android（本仓库页面）
                 → 自动跳转 → img.yjtv.top 真实文件
```

## 文件结构

- `index.html` — 中转首页（说明页，直接访问不触发下载）
- `go/ios/index.html` — iOS 下载跳转页
- `go/android/index.html` — 安卓下载跳转页

## 换新包怎么改（关键）

1. **新安装包上传图床，必须用新文件名**（旧文件名会触发图床"文件受限"）
2. 修改对应跳转页里的 `location.replace("真实文件地址")`：
   - iOS：改 `go/ios/index.html` → 替换成新 ipa 地址
   - Android：改 `go/android/index.html` → 替换成新 apk 地址
3. 提交并推送：
   ```
   git add -A && git commit -m "更新下载地址" && git push
   ```
4. 等 1~2 分钟 GitHub Pages 生效
5. 可选：同步改落地页 `index.html` 里的时间戳文件名（TS_IOS / TS_AND）

## 相关链接

- 中转域名：https://1060404996.github.io/lwlive-dl/
- 落地页仓库：`1060404996/lwlive-landing` → https://1060404996.github.io/lwlive-landing/
- 图床后台：https://img.yjtv.top/dashboard
- App 后台（版本与公告）填的强制更新下载地址：
  - iOS：https://1060404996.github.io/lwlive-dl/go/ios
  - Android：https://1060404996.github.io/lwlive-dl/go/android

## 注意事项

- cloudns.org 免费域名被国内运营商 DNS 屏蔽，已弃用（2026-10）
- 中转页是 JS 跳转（`location.replace`），每次访问都执行，**不会缓存旧地址**（比 301 稳）
- 苹果跳浏览器打开中转链接 → 正常可用
- 安卓如果是"下载器直连"方式则**不能用中转页**（下载器拿到的是一整个网页），需填真实直链
