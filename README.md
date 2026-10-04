# 百查数据恢复大师 — 公共构建仓

本仓只保存构建工作流，应用源码位于私有 `myelnn/recovery`。参考 `myelnn/robovai-build` 的源码与打包分离方式。

**Validate release API** 使用同样的精确私有源码 SHA，验证发布权限、架构选择、独立 MySQL 迁移、网站浏览器流程与后台生产构建。该流程只执行测试，不部署服务或发布数据库记录，不上传源码和测试报告附件。

维护者通过 **Actions → Build desktop → Run workflow** 输入私有源码的完整 40 位提交 SHA。构建仓使用只读部署密钥，不能推送源码。工作流不会响应外部 PR，也不上传源码、源映射、测试镜像或依赖缓存。

目标：Windows x64/ia32，macOS 13+ Apple Silicon/Intel，Linux x64 AppImage/deb。完整矩阵全部通过后发布 [Releases](https://github.com/myelnn/recovery-build/releases) 测试版及 SHA256SUMS.txt；单平台构建保留 14 天 Artifacts。下载后可核对 SHA-256。

初期为镜像恢复测试版：支持平面 `.img/.dd/.raw`，Unix 设备直接恢复尚未开放。Mac 安装包未签名；正式分发需完成 Developer ID 签名和公证。镜像读取无需管理员权限，不能以 root 启动整个界面绕过授权。APFS/ext4 的专项恢复以应用能力表和测试报告为准。

**Verify downloaded installers** 校验已有测试包的字节、大小和源码身份，在一次性 runner 上验证真实安装/复制、生产 GUI 启动、原生引擎、镜像恢复和移除，并确认不删除用户数据。Mac 覆盖 DMG/ZIP 两架构，Linux 覆盖 DEB/AppImage，Windows 覆盖 x64/ia32 NSIS。该流程不发布版本；不能替代签名、公证或真实外接磁盘验收。

官网只展示验收通过的正式下载。beta 选择器默认关闭，仅隔离预览构建可显式开启；API 验证同时检查预览流程和官网禁止 beta 的中英文流程。已有测试包仍以 prerelease 保存，正式版须满足专项验收条件后另行构建发布。

后续测试版增加限定 ext4 元数据解析：可提取现存文件和保留可验证 extent 的删除候选，恢复碎片与稀疏区。原文件名缺失时使用生成名称；尚不包含 JBD2 历史、完整内核误删和 APFS 元数据恢复。Linux 构建使用 e2fsprogs 独立镜像验证原件哈希，并在安装包内重验生产 Worker 链。
