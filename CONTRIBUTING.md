# 贡献指南

欢迎为本项目贡献力量！提交前请确保遵循以下规范。

## 贡献范围

本仓库只维护文档（使用指南、功能状态与发布说明）。以下内容请提交到对应的系统构建仓库：

| 内容 | 仓库 |
|------|------|
| Ubuntu 镜像构建（rootfs / boot、构建参数、CI） | [code002-2/ubuntu-sheng](https://github.com/code002-2/ubuntu-sheng) |
| Arch Linux ARM 镜像构建（PKGBUILD、设备功能包、CI） | [code002-2/archlinux-sheng](https://github.com/code002-2/archlinux-sheng) |
| Fedora 镜像构建 | [mumuxiao722/fedora-sheng](https://github.com/mumuxiao722/fedora-sheng) |
| NixOS 配置与镜像构建 | [DotRedstone/nixos-sheng](https://github.com/DotRedstone/nixos-sheng) |
| postmarketOS 镜像构建 | [alghiffaryfa19/sheng-pmos-builds](https://github.com/alghiffaryfa19/sheng-pmos-builds) |
| Debian 构建逻辑、内核与设备驱动 | 上游 [ianchb/debian-sheng](https://github.com/ianchb/debian-sheng)、[@map220v](https://github.com/map220v) |

## 提交 PR

1. Fork 本仓库
2. 创建特性分支 (`git checkout -b feature/my-feature`)
3. 提交更改 (`git commit -m 'Add: my feature'`)
4. 推送到分支 (`git push origin feature/my-feature`)
5. 打开 Pull Request

## 安全检查清单

提交 PR 前请确认：

- [ ] 未将镜像、编译产物或大体积二进制文件提交到 git
- [ ] 所有下载均使用 HTTPS
- [ ] 不含任何硬编码的密码或密钥

## 代码审查

本项目使用 CODEOWNERS 机制，文档与仓库配置由 `@code002-2` 审查。
