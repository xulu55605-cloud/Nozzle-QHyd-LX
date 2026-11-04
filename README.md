# Qhyd 油嘴流量理论计算可视化工具（PWA）

油嘴流量 Qhyd 的理论计算、动态范围扫描、多边界曲线叠加对比、曲线族自动对比。
纯前端静态网页，可安装到电脑 / 手机桌面，**安装后断网也能使用**。

Author: LU Xu

## 功能

- 基准参数设定，实时显示基准 Qhyd（数字滚动 + 仪表盘）
- 动态范围扫描（BSFC油耗 / 功率 / 转速 / CA喷油持续期 / 轨压）
- 主图：渐变发光曲线、基准点脉动标记、十字准线实时读数
- 暂存多组边界，勾选后同图叠加对比；导出白底 PNG（内含全部边界参数）
- 曲线族自动对比：一次生成多条曲线（如 4 个轨压）
- 从客户 Excel 导入基准参数（B11 功率/转速、B15 油耗、B7 缸数、B27 轨压）
- 深色 / 浅色主题一键切换

## 部署到 GitHub Pages

1. 新建一个 GitHub 仓库，把本文件夹里的**全部内容**上传到仓库根目录
   （`index.html`、`sw.js`、`manifest.webmanifest`、`vendor/`、`icons/`、`.nojekyll` 都要上传；
   注意 `.nojekyll` 是以点开头的隐藏文件，网页拖拽上传时容易漏掉，建议用 Git 命令行或 GitHub Desktop）。
2. 仓库 **Settings → Pages**，Source 选 **Deploy from a branch**，Branch 选 `main`，目录选 `/ (root)`，保存。
3. 等待一两分钟，访问 `https://<你的用户名>.github.io/<仓库名>/`。

命令行示例：

```bash
git init
git add .
git commit -m "Add Qhyd PWA"
git branch -M main
git remote add origin https://github.com/<你的用户名>/<仓库名>.git
git push -u origin main
```

## 安装与使用

- **电脑（Chrome / Edge）**：打开网址后，地址栏右侧出现"安装"图标，点击即可安装为独立窗口应用。
- **安卓（Chrome）**：菜单 → 添加到主屏幕 / 安装应用。
- **iPhone / iPad（Safari）**：分享按钮 → 添加到主屏幕。
- 首次联网打开后，所有文件已缓存到本机，之后可完全离线使用。

> PWA 与 Service Worker 只能在 `https://` 或 `localhost` 下工作。
> 直接双击 `index.html`（`file://`）仍可正常使用全部计算功能，只是没有安装和离线缓存能力。

## 本地预览

```bash
python3 -m http.server 8080
# 浏览器打开 http://localhost:8080
```

## 更新版本

修改了页面内容后，打开 `sw.js`，把顶部的 `CACHE_VERSION`（如 `qhyd-v6-1`）改成新值（如 `qhyd-v6-2`）再提交。
用户下次联网打开时会自动换上新版本；不改版本号的话，已安装的用户会一直使用旧缓存。

## 目录结构

```
index.html              主页面（全部逻辑）
sw.js                   Service Worker（离线缓存）
manifest.webmanifest    PWA 清单
icons/                  应用图标（含 maskable 与 iOS 图标）
vendor/                 本地化的第三方库（离线必需）
  chart.umd.js          Chart.js 4.6.1（MIT）
  xlsx.full.min.js      SheetJS 0.18.5（Apache-2.0）
.nojekyll               禁用 GitHub Pages 的 Jekyll 处理
```

## 第三方库许可

- Chart.js — MIT，见 `vendor/LICENSE-chartjs.md`
- SheetJS Community Edition — Apache-2.0，见 `vendor/LICENSE-sheetjs.txt`
