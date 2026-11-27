# 寄生虫 Parasite · 发布源

本地 + 云端双模 AI 助手「寄生虫」的安装包与在线升级源。

## 当前版本：1.0.1

**稳定性修复（重点）**

- 双层进程结构：父进程是守护进程，界面 + 服务在子进程里跑；子进程崩了 3 秒后自动拉起，5 分钟内连续崩 5 次才放弃并写日志，不再"话说一半整只消失"
- 移除了托盘（pystray），实测它触发的 Win32 用户回调异常 `0xC000041D` 就是闪退元凶
- 关闭窗口 = 隐藏，后台服务、语音、模型都不中断；再双击程序会把窗口叫回来（不会开出第二个实例）
- 崩溃现场写入 `%LOCALAPPDATA%\Parasite\crash.log`，出问题可直接看这个文件
- 正常退出走 `POST /api/app/quit`（守护进程会关掉子进程并收尾）

**台湾腔音色**

新增 `twmei`（台妹，zh-TW-HsiaoChen，语速 +12%、音调 +18Hz）、`twmei2`（机车妹，zh-TW-HsiaoYu，+14% / +22Hz，默认）、`twnan`（台男）。驾驶舱语音条可随时切换。

## 下载

| 平台 | 文件 | 说明 |
| --- | --- | --- |
| Windows | `Parasite-Setup-1.0.1.exe` | 安装版，双击安装，覆盖升级无需卸载 |
| Android | `Parasite-v1.0.1.apk` | 安卓 APP，装好后填电脑地址或云端地址 |

## 版本信息

`version.json` 是升级检查入口，程序每次启动/手动点「检查更新」会读它：

```json
{
  "version": "1.0.1",
  "win":     { "setup_url": "…Setup.exe", "sha": "…", "size": 79215387 },
  "android": { "url": "…apk", "sha": "…" },
  "mirror":  { "win": "…", "android": "…" }
}
```

## 安装包不含模型

安装包只有程序本体（约 79MB）。模型来源在首次启动的引导页里二选一：

- **本地**：llama.cpp 的 `llama-server`（默认 `127.0.0.1:8085`），可自动检测已有模型目录
- **云端**：任意 OpenAI 兼容接口（base_url + key + model），填完点「测试连接」即验证

## 升级方式

- 电脑端：驾驶舱点「⬆ 检查更新」，确认后自动下载 → sha256 校验 → 静默安装 → 自动重启
- 手机端：APP 右上「⋯」→「检查更新」，下载后直接覆盖安装，数据不丢

## 双仓库

- GitHub：<https://github.com/tangjie11685-rgb/parasite-update>
- Gitee：镜像仓库，国内加速（见 version.json 的 `mirror` 字段）
