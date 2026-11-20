# Baltar runner

The container image that Baltar runners use to run coding agents on your tasks. Baltar starts a
runner from this image when a task is waiting, gives it that one task, and removes it when the task
ends. You don't need to pull or build it yourself; Baltar's provisioners do that for you.

## What's inside

- A slim Debian base with Node.js, Git and Python
- The open-source coding agents Codex CLI and OpenCode, installed unmodified at pinned versions
- Baltar's runner, which takes a task, runs the agent and reports back

Claude Code and the Cursor CLI are not included. When a runner group offers them, the runner
downloads them from their vendors at pinned versions and checks each download before use.

## Security and your data

- **One task per container.** Each task runs in a fresh container that is removed when the task
  ends. Nothing from one task is left for the next, and nothing is shared between organizations.
- **No credentials in the image.** The image holds no keys, tokens or passwords. A task receives
  only the secrets its runner group was given, and only while that task runs.
- **The agent runs without privileges.** The coding agent and your repository's commands run as an
  unprivileged user with no extra Linux capabilities.
- **Changes are proposed, not applied.** Changes the agent makes in Baltar wait for review before
  they take effect. What the agent can do in your repositories depends on the access you give the
  runner group.
- **Logs are scrubbed.** Before a task's logs are kept, its secret values and credentials are
  removed from them.

## Tags

`kit-<n>` is the newest image for runner version *n*. Baltar pins every runner to an exact image
digest, so a tag moving never changes a runner that is already running.
