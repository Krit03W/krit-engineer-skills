# Upstream

`SKILL.md` is vendored unchanged from [NVIDIA/SkillSpector](https://github.com/NVIDIA/SkillSpector)
(`skills/skill-inspector/SKILL.md`) at commit
`a09091e0ebf6c96ff327457529d7b0d372125884` (2026-11-16).
Apache License 2.0 — see [LICENSE](LICENSE). Upstream ships no NOTICE file.

Only the skill is vendored, not the scanner. The skill runs the
`skillspector` CLI when it is installed and falls back to a manual,
semantic-only review when it is not. To get the static scan, install the
CLI separately (Python 3.12/3.13):

```bash
uv tool install --python 3.13 git+https://github.com/NVIDIA/skillspector.git
```

To update: copy `skills/skill-inspector/SKILL.md` from upstream over this
folder's `SKILL.md`, then bump the commit above.
