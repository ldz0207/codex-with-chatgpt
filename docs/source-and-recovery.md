# Source and locked recovery / 来源与锁定恢复

This fork and an existing upstream deployment are separate sources. Choose the source recorded for the target deployment before using the upstream quick-install/update workflow. This document records source metadata; it does not claim the fork and upstream are interchangeable or authorize switching an existing backend.

## Recorded sources (2026-10-22)

| Role | Source | Recorded commit | Package version |
| --- | --- | --- | --- |
| This personal fork's main before this documentation repair | [ldz0207/codex-with-chatgpt](https://github.com/ldz0207/codex-with-chatgpt) | `a9f91cd98df1bc82686f57d5bc2b2993394c93be` | 0.1.1 |
| Existing LDZ_AI checkout, read-only metadata verification | [XiaoDuoYa/codex-with-chatgpt](https://github.com/XiaoDuoYa/codex-with-chatgpt) | [`9663b88753e35c76796c5bce000293e0bd22cd9e`](https://github.com/XiaoDuoYa/codex-with-chatgpt/commit/9663b88753e35c76796c5bce000293e0bd22cd9e) | 0.1.3 |

The existing checkout's origin is `https://github.com/XiaoDuoYa/codex-with-chatgpt.git`, and its working tree was clean at inspection. This is source evidence only; no backend, connector, installed Skill or authentication state was changed or retested. Another device must identify its own source and current state.

## Lockfile boundary

Both recorded commits contain the same `pnpm-lock.yaml` Git blob (`88336be7db815addbbd67c86bda9713cc57d284d`). Its repository bytes use LF, with SHA-256:

`6ee9a7f0261dc2b53329f38ebe259832a61ff5472ea15d48cb486f40e2ec6a6b`

The recorded Windows checkout used CRLF and therefore had SHA-256 `70df031d08ddc23feada47a7c8c820b12fb921874f2285f6a00367309d4fa5fb`. Compare the same byte representation; a checkout's line-ending conversion changes its byte hash without changing the pinned lockfile content.

Their recorded package metadata declares Node.js `>=20` and `pnpm@11.24.0`; the lock format is 9.0. The SDK's manifest specifier is `latest`, while this lock resolves `@modelcontextprotocol/sdk` to 1.30.0. An unlocked install or a later `git pull` can select different code/dependencies. Equal lock hashes do not prove equal source behavior or successful installation on another device.

## Recovery sequence

1. Read the target deployment's `git remote get-url origin`, `git rev-parse HEAD`, and `git status --short`; record source, commit, local changes and lockfile hash. Review local changes in place. Do not automatically stash, reset, switch origin or upgrade a pinned checkout.
2. In a new isolated directory, obtain the chosen source and check out its recorded commit. For the existing LDZ_AI deployment, the reference source is the upstream row above; choosing this fork is a separate change. The date-stamped rows describe the pre-repair sources, not a moving “latest”.
3. Check the chosen commit's runtime and package-manager requirements. When dependency installation/build is authorized, use its committed lockfile with `corepack pnpm install --frozen-lockfile`, then `corepack pnpm build`. If the lock is incompatible, stop and review instead of regenerating it silently. These commands were documented, not executed during this repair.
4. Restore the installed Skill's checkout-path reference, host registration and required configuration using the target device's existing process. OAuth/Cloudflare credentials, browser sessions, active databases and tokens stay outside Git. Use normal target-device authentication rather than copying secrets or active app state.
5. Verify bridge startup, source/workspace boundary, authenticated read access and the intended review loop on the target device. Source checkout, dependency lock and documentation checks alone are not this functional acceptance.

The automatic update policy described in the upstream README/Skill is an upstream workflow, not permission to upgrade a pinned recovery or synchronize this fork. Update checks, review of a chosen version, dependency installation, connector repair and backend changes are separate operations. This repair changes documentation only and performs none of them.

中文边界：个人 fork、已有上游部署和“最新版本”分开记录；恢复以目标部署的来源、提交与锁文件为准。本机配置和认证状态不上传本仓；另一设备的安装、登录、工具发现与实际功能仍分别验收。
