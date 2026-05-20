# Claude Code — Official Reference

## Official Docs

| Topic | URL |
|-------|-----|
| CLAUDE.md / Memory | https://code.claude.com/docs/en/memory.md |
| Slash Commands | https://code.claude.com/docs/en/commands.md |
| Hooks | https://code.claude.com/docs/en/hooks.md |
| Skills | https://code.claude.com/docs/en/skills.md |
| Best Practices | https://code.claude.com/docs/en/best-practices.md |
| Common Workflows | https://code.claude.com/docs/en/common-workflows.md |
| Output Styles | https://code.claude.com/docs/en/output-styles.md |

---

## Memory (CLAUDE.md)

### Scope levels (loaded in order)

| Level | Path | Shared? |
|-------|------|---------|
| Managed | `/Library/Application Support/ClaudeCode/CLAUDE.md` | Org-wide |
| User | `~/.claude/CLAUDE.md` | All projects |
| Project | `./CLAUDE.md` or `./.claude/CLAUDE.md` | Yes (git) |
| Local | `./CLAUDE.local.md` | No (gitignored) |

### Path-scoped rules

```markdown
<!-- .claude/rules/api.md -->
---
paths:
  - "src/api/**/*.ts"
  - "*.md"
---
# Rules that only apply to matching files
```

### Import other files

```markdown
@README.md
@docs/git-instructions.md
```

### Auto-memory

- Stored at `~/.claude/projects/<project>/memory/`
- First 200 lines or 25KB of `MEMORY.md` loaded automatically
- Topic files loaded on-demand
- Claude maintains this; you can edit or delete anytime
- Run `/memory` to verify what's loaded

### Good CLAUDE.md content

✅ Include: build commands, code style, testing instructions, architectural decisions, quirks  
❌ Exclude: things Claude can infer from code, standard conventions, long tutorials

Keep under 200 lines per file. Specific and verifiable beats vague.

---

## Commands

### Setup
| Command | What it does |
|---------|-------------|
| `/init` | Generate starter `CLAUDE.md` |
| `/memory` | View/edit loaded memory files |
| `/mcp` | Configure MCP servers |
| `/permissions` | Set approval rules |
| `/plugin` | Browse and install plugins |

### During work
| Command | What it does |
|---------|-------------|
| `/plan` | Switch to plan mode (propose before editing) |
| `/model` | Switch models |
| `/effort` | Adjust reasoning level |
| `/context` | View context window usage |
| `/compact` | Summarize conversation history |
| `/btw` | Quick aside that doesn't bloat history |
| `/rewind` | Restore to previous conversation state |
| `/clear` | Reset context between unrelated tasks |

### Parallel execution
| Command | What it does |
|---------|-------------|
| `/tasks` | List background tasks |
| `/agents` | Manage subagents |
| `/batch` | Large-scale changes across worktrees |
| `/background` | Detach session as background agent |
| `/worktree` | Create isolated parallel sessions |

### Config & tools
| Command | What it does |
|---------|-------------|
| `/config` | Change settings (model, effort, output style) |
| `/skills` | Browse and manage skills |
| `/hooks` | View configured hooks |
| `/doctor` | Diagnose configuration issues |
| `/rename` | Name current session |
| `/resume` | Pick up a previous conversation |
| `/review` | Code review tool |
| `/security-review` | Security audit |

---

## Hooks

### Lifecycle events

| Event | When |
|-------|------|
| `SessionStart` | Session begins/resumes |
| `SessionEnd` | Session ends |
| `UserPromptSubmit` | Before Claude processes prompt |
| `PreToolUse` | Before tool call executes |
| `PostToolUse` | After tool call succeeds |
| `PermissionRequest` | Permission dialog appears |
| `Stop` | Claude finishes responding |
| `StopFailure` | Claude fails to stop cleanly |
| `FileChanged` | Watched file changes on disk |
| `WorktreeCreate` | Worktree is created |

### Hook types

**Command hook**
```json
{
  "type": "command",
  "command": "script.sh",
  "args": ["arg1"],
  "timeout": 30,
  "statusMessage": "Running validation..."
}
```
With `args` = exec (no shell). Without `args` = shell (supports pipes, `&&`, globs).

**HTTP hook**
```json
{
  "type": "http",
  "url": "http://localhost:8080/hooks/endpoint",
  "headers": { "Authorization": "Bearer $MY_TOKEN" },
  "allowedEnvVars": ["MY_TOKEN"],
  "timeout": 30
}
```

**MCP tool hook**
```json
{
  "type": "mcp_tool",
  "server": "my_server",
  "tool": "security_scan",
  "input": { "file_path": "${tool_input.file_path}" }
}
```

**Prompt hook** — LLM yes/no decision  
**Agent hook** — Subagent with tool access (experimental)

### Config locations

| Location | Path | Shared? |
|----------|------|---------|
| User | `~/.claude/settings.json` | All projects |
| Project | `.claude/settings.json` | Yes (git) |
| Project local | `.claude/settings.local.json` | No |
| Plugin | `<plugin>/hooks/hooks.json` | Plugin only |

### Exit code behavior

| Code | Meaning |
|------|---------|
| `0` | Success; parse JSON from stdout |
| `2` | Blocking error; show stderr to Claude |
| other | Non-blocking; log and continue |

### JSON output format

```json
{
  "continue": true,
  "suppressOutput": false,
  "systemMessage": "Warning message",
  "decision": "block|allow|ask|defer",
  "reason": "Why this decision",
  "hookSpecificOutput": {
    "hookEventName": "PreToolUse",
    "additionalContext": "Context for Claude",
    "permissionDecision": "deny|allow|ask|defer"
  }
}
```

### Path placeholders

- `${CLAUDE_PROJECT_DIR}` — Project root
- `${CLAUDE_PLUGIN_ROOT}` — Plugin install directory
- `${CLAUDE_PLUGIN_DATA}` — Plugin persistent data

### Common use cases

1. Security — Block destructive commands
2. Context injection — Load branch name, CI status, issue data
3. Permission automation — Auto-approve safe ops
4. Environment setup — Inject env vars per project
5. Compliance — Audit tool usage externally
6. File watching — React to config file changes

---

## Skills

### Where skills live

| Scope | Path |
|-------|------|
| Personal | `~/.claude/skills/<name>/SKILL.md` |
| Project | `.claude/skills/<name>/SKILL.md` |
| Plugin | `<plugin>/skills/<name>/SKILL.md` |

### Directory structure

```
my-skill/
├── SKILL.md           # Main instructions (required)
├── template.md        # Template for Claude to fill
├── examples/
│   └── sample.md
└── scripts/
    └── validate.sh
```

### SKILL.md frontmatter

```yaml
---
name: my-skill
description: What this skill does; when Claude should use it
disable-model-invocation: true  # Only manual invocation
user-invocable: false           # Only auto-invocation
allowed-tools: Read Grep Bash(git status *)
context: fork                   # Run in isolated subagent
agent: Explore                  # Which subagent type
model: opus
effort: high
paths:
  - "src/**/*.ts"               # Only load for matching files
argument-hint: "[issue-number]"
arguments: [issue, branch]
---
```

### String substitutions

| Placeholder | Value |
|------------|-------|
| `$ARGUMENTS` | All arguments |
| `$ARGUMENTS[N]` or `$N` | Nth argument (0-indexed) |
| `$name` | Named arg from `arguments` list |
| `${CLAUDE_SESSION_ID}` | Current session ID |
| `${CLAUDE_EFFORT}` | Current effort level |
| `${CLAUDE_SKILL_DIR}` | Skill directory path |

### Dynamic context injection

```markdown
## Environment
!`node --version`
!`git branch --show-current`

## Multi-line
```!
git status --short
npm ls --depth=0
```
```

Runs before Claude sees the skill. Output replaces placeholder.

### Memory budget

- Auto-compaction keeps first 5,000 tokens per skill
- All skills share 25,000-token combined budget
- Re-invoke after compaction if skill content dropped

### Bundled skills

| Skill | What it does |
|-------|-------------|
| `/run` | Launch and drive the app |
| `/verify` | Confirm a code change works |
| `/simplify` | Review code for quality |
| `/batch` | Large-scale changes across worktrees |
| `/loop` | Run prompt on recurring interval |
| `/schedule` | Create scheduled remote agents |
| `/claude-api` | Build/debug Claude API apps |
| `/review` | Code review |
| `/security-review` | Security audit |
| `/debug` | Enable debug logging |

---

## Output Styles

### Built-in styles

| Style | Behavior |
|-------|----------|
| `Default` | Standard software engineering mode |
| `Proactive` | Act immediately, assume reasonable defaults |
| `Explanatory` | Adds "Insights" explaining implementation choices |
| `Learning` | Adds `TODO(human)` markers; collaborative mode |

### Change style

```json
// .claude/settings.local.json
{ "outputStyle": "Explanatory" }
```
Or run `/config` → Output style.

### Custom style file

```yaml
---
name: My Style
description: What it does
keep-coding-instructions: true   # keep Claude's coding system prompt
force-for-plugin: false
---

Additional instructions appended to system prompt...
```

Locations: `~/.claude/output-styles/name.md` (user) or `.claude/output-styles/name.md` (project).

---

## Best Practices

### Context is your most important resource

Context window fills fast and performance degrades as it fills.

### Core workflow

1. **Explore** (plan mode) — Read files, no changes
2. **Plan** (plan mode) — Detailed plan; edit in editor
3. **Implement** (default) — Code, run tests, fix failures
4. **Commit** — Commit + PR

> Skip planning for small fixes (typo, rename, single line).

### Always give Claude a way to verify

Without tests or expected output, Claude might produce plausible-looking but broken code. You become the only feedback loop.

### Session management

| Action | Command / Key |
|--------|--------------|
| Stop mid-action | `Esc` |
| Restore previous state | `Esc + Esc` or `/rewind` |
| Reset between tasks | `/clear` |
| Summarize history | `/compact` |
| Quick aside | `/btw` |
| Resume last session | `claude --continue` |
| Pick session | `claude --resume` |

### Common failure patterns

| Pattern | Fix |
|---------|-----|
| Unrelated tasks fill context | `/clear` between tasks |
| Repeated corrections pollute context | `/clear` + write better prompt |
| Over-specified CLAUDE.md | Ruthlessly prune |
| No way to verify correctness | Always provide tests or expected output |
| Claude reads hundreds of files | Scope narrowly or use subagents |

### Automation

```bash
# Non-interactive (CI/scripts)
claude -p "prompt"                        # plain text output
claude -p "prompt" --output-format json   # JSON output
claude -p "prompt" --permission-mode auto # no interruptions
```

---

## Feature Comparison

| Feature | Scope | Use when | Best for |
|---------|-------|----------|---------|
| **CLAUDE.md** | Persistent / session | Every project | Conventions, build commands, code style |
| **Auto-memory** | Per-repo | Patterns Claude learns over time | Insights, debugging patterns |
| **`.claude/rules/`** | Path-scoped | Different standards per file type | API rules, test rules |
| **Skills** | Reusable workflow | Repeatable tasks | Investigations, deployments, codegen |
| **Hooks** | Lifecycle automation | Must happen reliably | Validation, linting, env setup |
| **Subagents** | Isolated context | Deep investigation, parallel work | Context-heavy exploration |
| **Output styles** | System prompt | Different tone/role | Educational, data analysis, writing |
| **Plugins** | Bundle of extensions | Distribute across team | Skills + hooks + agents as one package |

---

## Quick Tips

- `memory.md` → CLAUDE.md structure, aliases, instructions
- `commands.md` → custom slash commands (type `/yourcommand`)
- `skills.md` → reusable skills with full logic

> **Prompt aliases** (like `@alias`) are NOT an official feature — Claude just reads CLAUDE.md and follows patterns. **Skills** are the proper version with code/logic.
