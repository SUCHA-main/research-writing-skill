# Installing Research Writing Assistant for OpenCode

本仓库是一个 Agent Skills 集合，不是可由 `opencode.json` 的 `plugin` 字段
安装的 npm 插件。OpenCode 会从 `~/.config/opencode/skills/<name>/SKILL.md`
发现全局技能，因此应逐个链接 `skills/` 下的目录。

## 前置要求

- [OpenCode](https://opencode.ai) 已安装
- Git
- 支持符号链接的 shell，或 Windows PowerShell 的目录连接

## macOS / Linux

```bash
git clone https://github.com/SUCHA-main/research-writing-skill.git \
  "$HOME/.config/opencode/research-writing-skill"
mkdir -p "$HOME/.config/opencode/skills"

for skill_dir in "$HOME/.config/opencode/research-writing-skill"/skills/*; do
  if [ -f "$skill_dir/SKILL.md" ]; then
    ln -sfn "$skill_dir" "$HOME/.config/opencode/skills/$(basename "$skill_dir")"
  fi
done
```

## Windows (PowerShell)

```powershell
$repo = "$env:USERPROFILE\.config\opencode\research-writing-skill"
$skillsRoot = "$env:USERPROFILE\.config\opencode\skills"

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

重启 OpenCode，在会话中使用原生 `skill` 工具列出技能，并确认至少能发现：

- `using-research-writing`
- `paper-orchestration`
- `evidence-driven-writing`

加载时使用技能目录名，不要使用旧文档中的
`research-writing/brainstorming-research` 形式。

## 更新

```bash
cd "$HOME/.config/opencode/research-writing-skill"
git pull --ff-only
```

符号链接或目录连接仍指向同一克隆目录，不需要重新创建。

## 故障排除

1. 确认目标技能目录中存在 `SKILL.md`。
2. 确认链接指向当前仓库的 `skills/<name>/` 目录。
3. 使用 OpenCode 原生 `skill` 工具重新列出技能。
4. 如果仍无法发现，核对当前 OpenCode 版本的 Agent Skills 文档。

## 来源与帮助

- 当前 fork：https://github.com/SUCHA-main/research-writing-skill
- 问题反馈：https://github.com/SUCHA-main/research-writing-skill/issues
- 原始上游：https://github.com/Norman-bury/research-writing-skill
