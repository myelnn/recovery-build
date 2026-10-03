# 百查数据恢复大师 — 公共构建仓

本仓只保存构建工作流，应用源码位于私有 `myelnn/recovery`。参考 `myelnn/robovai-build` 的源码与打包分离方式。

维护者通过 **Actions → Build desktop → Run workflow** 输入私有源码的完整 40 位提交 SHA。构建仓使用只读部署密钥，不能推送源码。工作流不会响应外部 PR，也不上传源码、源映射、测试镜像或依赖缓存。

目标：Windows x64/ia32，macOS 13+ Apple Silicon/Intel，Linux x64 AppImage/deb。下载成功运行的 Artifacts 后核对 SHA256SUMS.txt。

初期 Mac 安装包为未签名测试版；正式分发需完成 Developer ID 签名和公证。Linux 镜像读取无需管理员权限；设备权限受系统控制，不能以 root 启动整个界面绕过授权。APFS/ext4 的专项恢复以应用能力表和测试报告为准。
