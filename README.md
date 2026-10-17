# 映真 Restore Studio

本地 GPU 视频去马赛克工具。自动检测马赛克区域（YOLO），BasicVSR++ 重建修复，输出保持原分辨率，音轨自动合并。

> 仅供学习研究与自有素材处理，请遵守当地法律法规。

## 下载

到 [Releases](https://github.com/ceoifung/restore-studio-pub/releases) 下载最新版本（当前 v0.3.0）。

| 包 | 说明 |
|---|---|
| `RestoreStudio-windows-cuda.zip.001/.002` | Windows NVIDIA 显卡版（全部分卷都要下载） |
| `RestoreStudio-linux-cuda.tar.gz.part00~02` | Linux NVIDIA 显卡版（全部分卷都要下载） |

**为什么分卷**：GitHub 单文件上限 2GB，CUDA 版体积超过需要拆分。

### 合并解压

**Windows**：把 `.zip.001` `.zip.002` 放同一目录，用 [7-Zip](https://www.7-zip.org/) 或 WinRAR 解压第一个分卷（`.zip.001`）即可。

**Linux**：

```bash
cat RestoreStudio-linux-cuda.tar.gz.part* > RestoreStudio.tar.gz
tar xzf RestoreStudio.tar.gz
```

## 系统要求

- **CUDA 版**：NVIDIA 显卡 + 较新驱动（CUDA 12.x 支持，建议 525+）；无需安装 CUDA 工具包，运行库已内置
- Windows 10/11 或 Linux（Debian 11+ / Ubuntu 22.04+，glibc ≥ 2.35）
- 磁盘空间：解压后约 8GB
- 无 NVIDIA 显卡请等待 CPU 版发布，或自行下载源码构建（见下）

## 使用

解压后双击运行（Windows `RestoreStudio.exe` / Linux `./RestoreStudio`）：

- 拖入视频 → 开始处理；内嵌播放器直接预览成品
- 支持批量后台处理、只看检测框模式
- 检测/修复模型已内置，无需另外下载

命令行自检（排查环境问题）：

```bash
RestoreStudio --selftest              # 导入链自检，退出码 0 即正常
RestoreStudio --process 视频路径       # 无界面处理一个视频
RestoreStudio --process 视频路径 --detect-only   # 只看检测框，秒出
```

## 常见问题

- **处理速度慢/报 CUDA 错误**：确认已安装 NVIDIA 显卡驱动；界面左下角设备选 `cuda:0`
- **WSL 下启动黑屏/崩溃**：`LIBGL_ALWAYS_SOFTWARE=1 QT_OPENGL=software ./RestoreStudio`（WSLg 的 EGL 兼容问题）
- **音轨合并失败**：日志会明确提示，输出为无声视频，可用 ffmpeg 手动合并

## 关于本仓库

这是**自动构建发布通道**：源码在私有仓库，打版本 tag 后由 GitHub Actions 自动双平台构建（Nuitka 编译，源码保护）并发布到 Release。本仓库不包含源码。
