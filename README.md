# deps-archive

Original build inputs for
[xiaomipad-8pro-mainline](https://github.com/yzddmr6/xiaomipad-8pro-mainline)
and
[onepluspad-2pro-mainline](https://github.com/yzddmr6/onepluspad-2pro-mainline).
The files are kept so that the builds still work if an upstream download
disappears.

## What is stored here

Only inputs that cannot be replaced by rebuilding from source:

- signed binaries, kept as the original files (the Windows guest drivers from
  Droid-VM keep their signatures only in the original ZIP);
- source archives whose exact bytes the build scripts check.

The files are release assets. Each asset is named
`<sha256>-<original file name>` and stored as downloaded, without
repacking. [manifest.json](manifest.json) lists every file with its size,
SHA-256, upstream location, source commit and license notes.

Releases only grow. New inputs go into a new release, and published assets
are never replaced or edited.

## What is not stored here

Inputs from kernel.org, Ubuntu and Debian snapshots, the Mesa archive,
Google, Mozilla and crates.io are pinned by version and SHA-256 in the
integration repositories and downloaded from those permanent addresses.

Git sources that we keep developing live in their own repositories with full
history:
[crosvm](https://github.com/yzddmr6/crosvm),
[edk2-gunyah](https://github.com/yzddmr6/edk2-gunyah),
[qualcomm-iris-vaapi](https://github.com/yzddmr6/qualcomm-iris-vaapi),
[libssc](https://github.com/yzddmr6/libssc),
[hexagonrpc](https://github.com/yzddmr6/hexagonrpc) and
[iio-sensor-proxy](https://github.com/yzddmr6/iio-sensor-proxy).

## How the builds use it

Each build looks for an input in this order: the local cache, our own copy
(this archive or the repositories above), then the pinned upstream address.
Every file is checked against its SHA-256, and a mismatch stops the build.
See `deps/README.md` in either integration repository.

## Licenses

Each file keeps the license of its upstream project. The license texts and
copyright notices are inside the archives or the corresponding source
archives. This repository adds no license terms of its own to them.

## 中文说明

本仓保存上面两个集成仓构建时用到、又无法靠源码重建替代的原始输入：签名驱动原件，以及构建脚本按字节校验的原始源码包。附件按 `<SHA-256>-<原文件名>` 命名，原样保存，不重新打包。[manifest.json](manifest.json) 记录每个文件的大小、哈希、上游地址、源码提交和许可说明。Release 只增不改，已发布的附件不会被替换。

kernel.org、Ubuntu/Debian 快照、Mesa、Google、Mozilla、crates.io 等机构来源只在集成仓里钉住版本和哈希，不在这里存档。需要继续开发的 Git 依赖放在上面列出的六个独立仓库里，保留完整历史。

构建按“本地缓存 → 我们的副本 → 上游固定地址”的顺序取文件，哈希不符立即停止。
