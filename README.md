# 寄生虫 Parasite · 发布源

本地 + 云端双模 AI 助手「寄生虫」的安装包与在线升级源。

## 下载

| 平台 | 文件 | 说明 |
| --- | --- | --- |
| Windows | `Parasite-Setup-1.0.0.exe` | 安装版，双击安装，首次启动带引导 |
| Windows | `Parasite-1.0.0-win.zip` | 绿色版，解压即用（程序内自升级用这个） |
| Android | `Parasite-v1.0.0.apk` | 安卓 APP，装好后填电脑地址或云端地址 |

## 版本信息

`version.json` 是升级检查入口，程序每次启动/手动点「检查更新」会读它：

```json
{
  "version": "1.0.0",
  "win":     { "url": "…win.zip", "setup_url": "…Setup.exe", "sha": "…" },
  "android": { "url": "…apk", "sha": "…" },
  "mirror":  { "win": "", "android": "" }
}
```

## 安装包不含模型

安装包只有程序本体（约 75MB）。模型来源在首次启动的引导页里二选一：

- **本地**：llama.cpp 的 `llama-server`（默认 `127.0.0.1:8085`），可自动检测已有模型目录
- **云端**：任意 OpenAI 兼容接口（base_url + key + model），填完点「测试连接」即验证

## 升级方式

- 电脑端：驾驶舱点「⬆ 检查更新」，或控制台里检查；确认后自动下载、替换、重启
- 手机端：APP 右上「⋯」→「检查更新」，下载后直接覆盖安装，数据不丢

## 双仓库

- GitHub：<https://github.com/tangjie11685-rgb/parasite-update>
- Gitee：镜像仓库，国内加速（见 version.json 的 `mirror` 字段）
