# Product Hunt launch draft

## Product details

**Name:** Codebase Brief

**Tagline (47/60 characters):** A repo map for coding chats without file access

**Short description (under 260 characters):** Turn a local repo and coding task into a short, reviewable Markdown map for browser-based AI chats. Inspect suggested files, copy useful excerpts and source paths. Free, open source, no AI calls.

**Product URL:** https://mohamed1111111m.github.io/codebase-brief/

**Topics:** Developer Tools, Open Source, Artificial Intelligence

**Pricing:** Free and open source

## Maker's first comment

I made Codebase Brief for the times I use a browser-based coding assistant that can’t inspect my local working tree. I wanted a reviewable way to bring it enough repository context to start a task.

The CLI reads a local repo, asks what you want to do, suggests a small set of files with reasons, and creates a Markdown brief with excerpts and paths you can check. It can use recent Git history and an optional base ref to prioritize changed files. It does not call an AI service or upload the repository.

This is an early tool. File selection is heuristic, so it can miss relevant code or include noise. I’d love feedback from developers who try it on a repository they know: what useful file did it miss, and what did it include unnecessarily?

Try it and see screenshots: https://mohamed1111111m.github.io/codebase-brief/ · Source and full details: https://github.com/mohamed1111111m/codebase-brief

## Gallery assets

Use these existing product visuals, in this order:

1. `docs/images/social-preview.png` — product thumbnail / social preview.
2. `docs/images/guided-menu.png` — actual colorful guided menu.
3. `docs/images/sample-context-brief.png` — generated brief example.

Use docs/images/product-hunt-demo.mp4 as a short, silent walkthrough assembled from the app's existing screenshots. It shows the real interface and output, but it is not a live screen recording.

## Launch goal and day plan

**Goal:** Get five developers to try the CLI on a repository they know and report which files were useful, missing, or irrelevant. Do not use rank, upvotes, or stars as the success measure.

- Before launch: finish the public install path, review this draft, and make sure the demo file plays and matches the current product.
- Launch day: publish at 12:01 AM Pacific only on a date when the maker can be around; respond to questions and criticism honestly.
- Share the Product Hunt page with relevant communities only where their rules allow it. Ask people to try it or leave feedback; never ask for votes.
- After launch: summarize feedback and decide whether file relevance, install friction, or another problem is the next improvement.

## Preflight checklist

- [ ] The latest `codebase-brief` release is on PyPI and installs from a clean environment.
- [ ] Demo video and all screenshots are readable at Product Hunt display size; replace the screenshot walkthrough with a live screen recording if one is available.
- [ ] Product Hunt account onboarding is complete and the maker profile is filled in.
- [ ] All links work; GitHub Actions and the local test suite are green.
- [ ] Maker is available to respond through launch day.
