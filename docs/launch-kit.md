# Codebase Brief launch kit

Codebase Brief is an early open-source tool. Its file selection uses simple heuristics; it has not been shown to improve coding-task success or save a measured amount of time. Keep launch posts specific and invite people to test the output on a repository they know.

## 45-second demo recording

The repository also includes a 12-second silent screenshot walkthrough at docs/images/product-hunt-demo.mp4. It uses the actual menu and generated-brief screenshots; it is not a recording of a live run. Prefer a live recording when you can capture one without showing private code or credentials.

Record a terminal window and show one complete path from repository to brief. Use a small public sample repository or a project you are allowed to show. Do not show private source, credentials, or personal paths.

1. **0–5 sec:** Show the repository and say: “I built Codebase Brief to make a compact, task-focused map of a codebase that I can review before giving it to a coding assistant.”
2. **5–12 sec:** Run `brief "C:\work\sample-app" --task "Trace the login flow" --base main --budget 1800` (replace the path and base ref with ones that exist).
3. **12–22 sec:** Show the suggested files and their selection reasons. Explain that the user can keep or change the selection.
4. **22–35 sec:** Show the generated brief: task, project overview, recent changes, selected-file excerpts, and source paths.
5. **35–45 sec:** Say: “It runs locally and makes no AI or network calls. Review the brief before sharing it; selection and secret filtering are best-effort.” Show the repository link.

Keep the terminal text large enough to read. Prefer a real run over a mockup. If recording a longer walkthrough, also show `brief --help` and the menu (`brief -i`).

## Show HN draft

Hacker News asks that Show HN projects be personally built, usable by visitors, and presented by someone available to discuss them. Edit this in your own voice and include what motivated you to make the tool and what you learned from testing it. Do not ask people to upvote.

**Title:** `Show HN: Codebase Brief – a local repo brief for browser-based coding chats`

**Draft:**

I made Codebase Brief for browser-based coding chats that cannot inspect my local working tree. I wanted a repeatable way to give one task a small, reviewable map of the relevant parts of a repository instead of copying files by hand.

It is a Python CLI. You point it at a local repo, describe a task, review the files it suggests and why, and get a Markdown brief with excerpts and source paths. Git history and an optional base ref help prioritize recent or changed files. It makes no AI calls and has no account or hosted service.

It is early, and file selection is heuristic rather than semantic. I would especially like feedback on files it misses or includes unnecessarily. The README has install steps and screenshots: https://github.com/mohamed1111111m/codebase-brief

## Short social post

When I use a browser-based coding chat, it cannot inspect the repo on my computer. I made Codebase Brief to pick a task-focused set of files, show why they were selected, and prepare a short brief I can review before pasting it into the chat.

No AI calls or account. File selection is heuristic, so I’m looking for developers to try it on a repo they know and tell me what it misses.

Try it: https://github.com/mohamed1111111m/codebase-brief

## Community post outline

Before posting to a subreddit, forum, or Discord, check that community’s current rules and use its project-sharing channel if it has one. Avoid copy-pasting the same promotion everywhere. Lead with the problem you personally had, describe the tool plainly, disclose that you made it, and ask one specific feedback question:

> I made a small local CLI to prepare a task-specific codebase brief for coding assistants. I’m trying to learn whether its suggested files are actually useful. If you try it on a repo you know, which important file did it miss (or include for no good reason)?

Link the README for installation and screenshots. Be available to answer questions and accept criticism; do not ask for votes or stars.

## Feedback to collect

For each tester, ask them to use the [tester feedback form](https://github.com/mohamed1111111m/codebase-brief/issues/new?template=tester-feedback.yml). It captures the task, install result, file-selection changes, and whether the brief helped without asking them to share private source code. Ask:

1. What task and repository did you try it on? (They should not share private code.)
2. Which suggested files were useful, missing, or irrelevant?
3. Did the brief make it easier to orient your coding assistant? What did you still have to explain manually?
4. Which OS and Python version did you use? Did installation work from a clean environment?

Record observations, not just stars or downloads. A few detailed examples of missed and unnecessary files are more useful for deciding what to build next.
