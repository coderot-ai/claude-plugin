# coderot for Claude Code

Before Claude adds code to a file, this plugin checks whether the file is one to be careful with. It reads your repo's git
history on your machine with [coderot](https://coderot.ai/?utm_source=claude-plugin)'s CLI and names three kinds of file:

- **Files agents keep growing:** most of their recent PRs came from AI agents. Claude puts new code in a new file next to them.
- **Hotspots:** high cognitive complexity and many commits in the last 90 days. Claude prefers a new module next to them.
- **Rising:** the files whose complexity rose most in about 30 days. Claude keeps new code out of them where it can.

Nothing is uploaded: the skill runs `npx -y @coderot-ai/cli hotspots --json` in your repo and reads its output.

## Install

```sh
claude plugin marketplace add coderot-ai/claude-plugin
claude plugin install coderot@coderot-ai
```

Claude uses the skill on its own before it edits or refactors existing files. You can also run it as `/coderot:hotspots`.

It needs Node.js and the repo's full history (a shallow clone gives a short list). On a large repo the first run takes a few
minutes, so Claude runs it once per session. To keep the list in the repo for every agent, run
`npx -y @coderot-ai/cli hotspots --md` and paste the block into `CLAUDE.md` or `AGENTS.md`; the skill uses that block while
it's less than a week old.

## The dashboard

The same numbers, tracked over time and per agent, with a PR comment from the GitHub Action:
[coderot.ai](https://coderot.ai/?utm_source=claude-plugin).

## License

[Elastic License 2.0](LICENSE)
