# Codex Auth Switch

一个用于快速切换多个 Codex 账号登录态的小工具。它不会重新登录，而是把不同账号的 `auth.json` 保存成 profile，需要切换时直接替换 `~/.codex/auth.json`。

## 安装

```bash
chmod +x ./codex-auth-switch
```

可选：放到 PATH 里。

```bash
mkdir -p ~/.local/bin
cp ./codex-auth-switch ~/.local/bin/
```

## 使用方式

最常用的切换方式：直接运行，不带参数。

```bash
./codex-auth-switch
```

它会显示已保存账号列表，输入数字即可切换：

```text
Codex profiles:
 1. * personal  personal@example.com
 2.   work      work@example.com

输入序号切换，或直接回车取消:
```

先手动登录第一个 Codex 账号，然后保存：

```bash
./codex-auth-switch add personal
```

再手动登录第二个 Codex 账号，然后保存：

```bash
./codex-auth-switch add work
```

之后可以通过菜单切换，也可以一行命令直接切换：

```bash
./codex-auth-switch switch personal
./codex-auth-switch switch work
```

## 常用命令

```bash
./codex-auth-switch
./codex-auth-switch ls
./codex-auth-switch whoami
./codex-auth-switch add work --force
./codex-auth-switch rm work --force
```

默认路径：

- Codex 登录态：`~/.codex/auth.json`
- profile 目录：`~/.codex/auth-profiles/`
- 切换前备份：`~/.codex/auth-profiles/.backups/`

## 安全说明

`auth.json` 和保存的 profiles 都是敏感登录凭据。工具会尽量把写入文件权限设为 `0600`，但仍建议：

- 不要把 profile 文件提交到 Git。
- 不要把 `~/.codex/auth-profiles/` 同步到不可信网盘。
- 如果某个账号不再使用，先在账号侧撤销会话，再删除对应 profile。

菜单会从本地 JWT payload 中解析邮箱；不会打印 token，也不会查询订阅类型或剩余额度。

## 自定义路径

```bash
./codex-auth-switch --auth /path/to/auth.json --profiles-dir /path/to/profiles save test
./codex-auth-switch --auth /path/to/auth.json --profiles-dir /path/to/profiles use test
```

## License

MIT
