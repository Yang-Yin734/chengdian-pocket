# 成电口袋 · 更新通道

这个仓库只做一件事：给「成电口袋」Android 应用提供**应用内更新**用的两样东西。

| 文件 | 作用 |
| --- | --- |
| `version.json` | 版本清单。App 冷启动读它，比本机新就弹窗提示。 |
| `apk/chengdian-pocket-<版本>.apk` | 对应的安装包，App 从这个仓库下载。 |
| `index.html` | 人看的下载页（GitHub Pages / jsDelivr 都能直接用）。 |

## App 里读的是哪两个地址

```
https://cdn.jsdelivr.net/gh/Yang-Yin734/chengdian-pocket@main/version.json
https://raw.githubusercontent.com/Yang-Yin734/chengdian-pocket/main/version.json
```

两个地址指向同一份 `main` 分支。App 会按顺序试，第一个返回 200 的就用；
jsDelivr 在国内通常更快，raw 作为兜底。

## 发新版本怎么做

1. 改 `app/build.gradle.kts` 的 `versionCode`（必须递增）和 `versionName`；
2. `gradle assembleRelease`；
3. 把 APK 拷成 `apk/chengdian-pocket-<新版本>.apk`；
4. 改 `version.json`：`versionCode` / `versionName` / `url` / `notes` / `sha256`（`Get-FileHash -Algorithm SHA256`）；
5. `git add -A && git commit -m "release <版本>" && git push`。

推上去之后，旧版本 App 下次打开就会自动弹窗提示更新。
jsDelivr 有几分钟缓存，急的话可以在清单地址后面加 `?t=时间戳`。

## 说明

- 应用是个人开发的非官方工具，数据来自电子科技大学教务系统，仅本人自用。
- 仓库里只放安装包和清单，不放任何学校账号、Cookie 或个人信息。