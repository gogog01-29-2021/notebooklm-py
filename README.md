NotebookLM을 “도구”로 쓰는 사람과 “시스템”으로 쓰는 사람의 차이

대부분의 사람들이 NotebookLM을 이렇게 씁니다.

유튜브 영상을 하나씩 붙여넣고,
PDF를 드래그앤드롭으로 올리고,
팟캐스트 버튼을 클릭하고 기다립니다.
동시에 Claude나 GPT에는 자료를 직접 붙여넣습니다.

컨텍스트가 꽉 차고, 토큰이 터지고, 결과가 잘립니다.
두 툴을 따로 쓰면서 둘 다 절반만 쓰고 있는 겁니다.

구조를 바꾸면 완전히 달라집니다.

notebooklm-py라는 오픈소스 라이브러리를 사용하면 NotebookLM을 에이전트의 도구로 직접 연결할 수 있습니다. Claude Code, Codex, 직접 만든 봇 모두 가능합니다.

1. 자료 수집 자동화
유튜브 50개짜리 플레이리스트도 코드 한 줄로 노트북에 전부 적재됩니다. PDF 폴더 전체도 마찬가지입니다. 손으로 하나씩 올리는 작업이 사라집니다.

2. 토큰 비용 구조 자체가 바뀝니다
기존 방식은 Claude가 자료 전체를 읽습니다. 새로운 구조에서는 NotebookLM이 자료를 담고 검색하고, 에이전트는 그 답변만 받아서 다음 작업을 실행합니다. Claude는 판단과 실행에만 토큰을 씁니다.

3. 웹 UI에서 불가능한 작업들
퀴즈와 플래시카드를 JSON으로 추출하거나, 마인드맵 데이터를 가져오거나, 슬라이드를 PPTX로 받는 것은 웹에서는 할 수 없습니다. 이 라이브러리를 통해서만 가능합니다.

4. 콘텐츠 생성 파이프라인 자동화
새 자료가 쌓이면 에이전트가 자동으로 팟캐스트를 생성하고 저장합니다. 매주 반복되는 작업을 스케줄러에 걸어두면 버튼을 누를 필요가 없습니다.

결국 이런 구조가 됩니다.
NotebookLM = 자료를 담고 검색하는 저장소
에이전트 = 판단하고 실행하는 두뇌
Claude = 토큰 낭비 없이 결론만 냅니다
AI를 쓴다고 했는데 알고 보니 내가 제일 열심히 일하고 있었던 건 아닐까요.

시스템이 일하게 만드는 것, 그게 진짜 AI 활용입니다.

비공식 라이브러리로 Google 업데이트에 따라 동작이 달라질 수 있습니다. 레포 링크는 첫 댓글에 달겠습니다.


# notebooklm-py
<p align="left">
  <img src="https://raw.githubusercontent.com/teng-lin/notebooklm-py/main/notebooklm-py.png" alt="notebooklm-py logo" width="128">
</p>

**A Comprehensive NotebookLM Skill & Unofficial Python API.** Full programmatic access to NotebookLM's features—including capabilities the web UI doesn't expose—via Python, CLI, and AI agents like Claude Code, Codex, and OpenClaw.

[![PyPI version](https://img.shields.io/pypi/v/notebooklm-py.svg)](https://pypi.org/project/notebooklm-py/)
[![Python Version](https://img.shields.io/badge/python-3.10%20%7C%203.11%20%7C%203.12%20%7C%203.13%20%7C%203.14-blue)](https://pypi.org/project/notebooklm-py/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Tests](https://github.com/teng-lin/notebooklm-py/actions/workflows/test.yml/badge.svg)](https://github.com/teng-lin/notebooklm-py/actions/workflows/test.yml)
<p>
  <a href="https://trendshift.io/repositories/19116" target="_blank"><img src="https://trendshift.io/api/badge/repositories/19116" alt="teng-lin%2Fnotebooklm-py | Trendshift" style="width: 250px; height: 55px;" width="250" height="55"/></a>
</p>

**Source & Development**: <https://github.com/teng-lin/notebooklm-py>

> **⚠️ Unofficial Library - Use at Your Own Risk**
>
> This library uses **undocumented Google APIs** that can change without notice.
>
> - **Not affiliated with Google** - This is a community project
> - **APIs may break** - Google can change internal endpoints anytime
> - **Rate limits apply** - Heavy usage may be throttled
>
> Best for prototypes, research, and personal projects. See [Troubleshooting](docs/troubleshooting.md) for debugging tips.

## What You Can Build

🤖 **AI Agent Tools** - Integrate NotebookLM into Claude Code, Codex, and other LLM agents. Ships with a root [NotebookLM skill](SKILL.md) for GitHub and `npx skills add` discovery, local `notebooklm skill install` support for Claude Code and `.agents` skill directories, and repo-level Codex guidance in [`AGENTS.md`](AGENTS.md).

📚 **Research Automation** - Bulk-import sources (URLs, PDFs, YouTube, Google Drive), run web/Drive research queries with auto-import, and extract insights programmatically. Build repeatable research pipelines.

🎙️ **Content Generation** - Generate Audio Overviews (podcasts), videos, slide decks, quizzes, flashcards, infographics, data tables, mind maps, and study guides. Full control over formats, styles, and output.

📥 **Downloads & Export** - Download all generated artifacts locally (MP3, MP4, PDF, PNG, CSV, JSON, Markdown). Export to Google Docs/Sheets. **Features the web UI doesn't offer**: batch downloads, quiz/flashcard export in multiple formats, mind map JSON extraction.

## Three Ways to Use

| Method | Best For |
|--------|----------|
| **Python API** | Application integration, async workflows, custom pipelines |
| **CLI** | Shell scripts, quick tasks, CI/CD automation |
| **Agent Integration** | Claude Code, Codex, LLM agents, natural language automation |

## Features

### Complete NotebookLM Coverage

| Category | Capabilities |
|----------|--------------|
| **Notebooks** | Create, list, rename, delete |
| **Sources** | URLs, YouTube, files (PDF, text, Markdown, Word, audio, video, images), Google Drive, pasted text; refresh, get guide/fulltext |
| **Chat** | Questions, conversation history, custom personas |
| **Research** | Web and Drive research agents (fast/deep modes) with auto-import |
| **Sharing** | Public/private links, user permissions (viewer/editor), view level control |

### Content Generation (All NotebookLM Studio Types)

| Type | Options | Download Format |
|------|---------|-----------------|
| **Audio Overview** | 4 formats (deep-dive, brief, critique, debate), 3 lengths, 50+ languages | MP3/MP4 |
| **Video Overview** | 3 formats (explainer, brief, cinematic), 9 visual styles, plus a dedicated `cinematic-video` CLI alias | MP4 |
| **Slide Deck** | Detailed or presenter format, adjustable length; individual slide revision | PDF, PPTX |
| **Infographic** | 3 orientations, 3 detail levels | PNG |
| **Quiz** | Configurable quantity and difficulty | JSON, Markdown, HTML |
| **Flashcards** | Configurable quantity and difficulty | JSON, Markdown, HTML |
| **Report** | Briefing doc, study guide, blog post, or custom prompt | Markdown |
| **Data Table** | Custom structure via natural language | CSV |
| **Mind Map** | Interactive hierarchical visualization | JSON |

### Beyond the Web UI

These features are available via API/CLI but not exposed in NotebookLM's web interface:

- **Batch downloads** - Download all artifacts of a type at once
- **Quiz/Flashcard export** - Get structured JSON, Markdown, or HTML (web UI only shows interactive view)
- **Mind map data extraction** - Export hierarchical JSON for visualization tools
- **Data table CSV export** - Download structured tables as spreadsheets
- **Slide deck as PPTX** - Download editable PowerPoint files (web UI only offers PDF)
- **Slide revision** - Modify individual slides with natural-language prompts
- **Report template customization** - Append extra instructions to built-in format templates
- **Save chat to notes** - Save Q&A answers or conversation history as notebook notes
- **Source fulltext access** - Retrieve the indexed text content of any source
- **Programmatic sharing** - Manage permissions without the UI

## Installation

```bash
# Basic installation
pip install notebooklm-py

# With browser login support (required for first-time setup)
pip install "notebooklm-py[browser]"
playwright install chromium
```

If `playwright install chromium` fails with `TypeError: onExit is not a function`, see the Linux workaround in [Troubleshooting](docs/troubleshooting.md#linux).

### Development Installation

For contributors or testing unreleased features:

```bash
pip install git+https://github.com/teng-lin/notebooklm-py@main
```

⚠️ The main branch may contain unstable changes. Use PyPI releases for production.

## Quick Start

<p align="center">
  <a href="https://asciinema.org/a/767284" target="_blank"><img src="https://asciinema.org/a/767284.svg" width="600" /></a>
  <br>
  <em>16-minute session compressed to 30 seconds</em>
</p>

### CLI

```bash
# 1. Authenticate (opens browser)
notebooklm login
# Or use Microsoft Edge (for orgs that require Edge for SSO)
# notebooklm login --browser msedge

# 2. Create a notebook and add sources
notebooklm create "My Research"
notebooklm use <notebook_id>
notebooklm source add "https://en.wikipedia.org/wiki/Artificial_intelligence"
notebooklm source add "./paper.pdf"

# 3. Chat with your sources
notebooklm ask "What are the key themes?"

# 4. Generate content
notebooklm generate audio "make it engaging" --wait
notebooklm generate video --style whiteboard --wait
notebooklm generate cinematic-video "documentary-style summary" --wait
notebooklm generate quiz --difficulty hard
notebooklm generate flashcards --quantity more
notebooklm generate slide-deck
notebooklm generate infographic --orientation portrait
notebooklm generate mind-map
notebooklm generate data-table "compare key concepts"

# 5. Download artifacts
notebooklm download audio ./podcast.mp3
notebooklm download video ./overview.mp4
notebooklm download cinematic-video ./documentary.mp4
notebooklm download quiz --format markdown ./quiz.md
notebooklm download flashcards --format json ./cards.json
notebooklm download slide-deck ./slides.pdf
notebooklm download infographic ./infographic.png
notebooklm download mind-map ./mindmap.json
notebooklm download data-table ./data.csv
```

Other useful CLI commands:

```bash
notebooklm auth check --test         # Diagnose auth/cookie issues
notebooklm agent show codex          # Print bundled Codex instructions
notebooklm agent show claude         # Print bundled Claude Code skill template
notebooklm language list             # List supported output languages
notebooklm metadata --json           # Export notebook metadata and sources
notebooklm share status              # Inspect sharing state
notebooklm source add-research "AI"  # Start web research and import sources
notebooklm skill status              # Check local agent skill installation
```

### Python API

```python
import asyncio
from notebooklm import NotebookLMClient

async def main():
    async with await NotebookLMClient.from_storage() as client:
        # Create notebook and add sources
        nb = await client.notebooks.create("Research")
        await client.sources.add_url(nb.id, "https://example.com", wait=True)

        # Chat with your sources
        result = await client.chat.ask(nb.id, "Summarize this")
        print(result.answer)

        # Generate content (podcast, video, quiz, etc.)
        status = await client.artifacts.generate_audio(nb.id, instructions="make it fun")
        await client.artifacts.wait_for_completion(nb.id, status.task_id)
        await client.artifacts.download_audio(nb.id, "podcast.mp3")

        # Generate quiz and download as JSON
        status = await client.artifacts.generate_quiz(nb.id)
        await client.artifacts.wait_for_completion(nb.id, status.task_id)
        await client.artifacts.download_quiz(nb.id, "quiz.json", output_format="json")

        # Generate mind map and export
        result = await client.artifacts.generate_mind_map(nb.id)
        await client.artifacts.download_mind_map(nb.id, "mindmap.json")

asyncio.run(main())
```

### Agent Setup

**Option 1 — CLI install**:

```bash
notebooklm skill install
```

Installs the skill into `~/.claude/skills/notebooklm` and `~/.agents/skills/notebooklm`.

**Option 2 — `npx` install** (via the open skills ecosystem):

```bash
npx skills add teng-lin/notebooklm-py
```

Fetches the canonical [SKILL.md](SKILL.md) directly from GitHub.


## Documentation

- **[CLI Reference](docs/cli-reference.md)** - Complete command documentation
- **[Python API](docs/python-api.md)** - Full API reference
- **[Configuration](docs/configuration.md)** - Storage and settings
- **[Release Guide](docs/releasing.md)** - Release checklist and packaging verification
- **[Troubleshooting](docs/troubleshooting.md)** - Common issues and solutions
- **[API Stability](docs/stability.md)** - Versioning policy and stability guarantees

### For Contributors

- **[Development Guide](docs/development.md)** - Architecture, testing, and releasing
- **[RPC Development](docs/rpc-development.md)** - Protocol capture and debugging
- **[RPC Reference](docs/rpc-reference.md)** - Payload structures
- **[Changelog](CHANGELOG.md)** - Version history and release notes
- **[Security](SECURITY.md)** - Security policy and credential handling

## Platform Support

| Platform | Status | Notes |
|----------|--------|-------|
| **macOS** | ✅ Tested | Primary development platform |
| **Linux** | ✅ Tested | Fully supported |
| **Windows** | ✅ Tested | Tested in CI |

## Star History

[![Star History Chart](https://api.star-history.com/image?repos=teng-lin/notebooklm-py&type=timeline&legend=top-left)](https://www.star-history.com/?repos=teng-lin%2Fnotebooklm-py&type=timeline&legend=top-left)

## License

MIT License. See [LICENSE](LICENSE) for details.
