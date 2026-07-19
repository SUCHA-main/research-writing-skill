# Installing Research Writing Assistant for Codex

通过 Codex 的 Agent Skills 发现机制启用本仓库中的各个技能。每个
`skills/<name>/` 目录都包含独立的 `SKILL.md`，因此需要逐个链接到
`~/.agents/skills/`。

## 前置要求

- Git
- 支持符号链接的 shell，或 Windows PowerShell 的目录连接

## macOS / Linux

```bash
git clone https://github.com/SUCHA-main/research-writing-skill.git \
  "$HOME/.codex/research-writing-skill"
mkdir -p "$HOME/.agents/skills"

for skill_dir in "$HOME/.codex/research-writing-skill"/skills/*; do
  if [ -f "$skill_dir/SKILL.md" ]; then
    ln -sfn "$skill_dir" "$HOME/.agents/skills/$(basename "$skill_dir")"
  fi
done
```

## Windows (PowerShell)

```powershell
$repo = "$env:USERPROFILE\.codex\research-writing-skill"
$skillsRoot = "$env:USERPROFILE\.agents\skills"

git clone https://github.com/SUCHA-main/research-writing-skill.git $repo
New-Item -ItemType Directory -Force -Path $skillsRoot | Out-Null

Get-ChildItem "$repo\skills" -Directory | Where-Object {
    Test-Path (Join-Path $_.FullName "SKILL.md")
} | ForEach-Object {
    $link = Join-Path $skillsRoot $_.Name
    if (-not (Test-Path -LiteralPath $link)) {
        New-Item -ItemType Junction -Path $link -Target $_.FullName | Out-Null
    }
}
```

如果目标目录已经存在，命令会保留它，不会覆盖。请先人工确认同名技能的
来源，再决定是否替换。

## 验证安装

重启 Codex 后，确认 `~/.agents/skills/` 下出现各技能目录，例如：

```bash
ls -la "$HOME/.agents/skills/using-research-writing"
ls -la "$HOME/.agents/skills/paper-orchestration"
```

每个目录中都应能看到 `SKILL.md`。随后可在对话中请求头脑风暴、文献综述
或论文结构规划，并确认 Codex 加载了对应技能。

## 更新

```bash
cd "$HOME/.codex/research-writing-skill"
git pull --ff-only
```

符号链接或目录连接仍指向同一克隆目录，不需要重新创建。

## 来源

- 当前 fork：https://github.com/SUCHA-main/research-writing-skill
- 原始上游：https://github.com/Norman-bury/research-writing-skill
