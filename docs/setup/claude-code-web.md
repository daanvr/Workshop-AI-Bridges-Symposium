# Set up Claude Code in the browser

A short, beginner friendly walkthrough for using **Claude Code on the web**:
an AI coding assistant that runs in the cloud. You do not install anything
on your computer. Everything happens in your browser, connected to a
**GitHub** repository.

By the end of this guide you will be able to:

1. Sign in to Claude Code on the web.
2. Connect it to GitHub.
3. Either create a brand new repository and start working in it, or
   connect it to a repository you already have.

If a step looks different in real life, the user interface may have changed
slightly since this guide was written (May 2026). The overall flow is the
same.

## What you need before starting

You need three things:

- A modern web browser (Chrome, Edge, Firefox or Safari).
- A **Claude account** with an active Pro, Max, Team or Enterprise plan.
  Claude Code on the web is not available on the free plan. You can sign
  up or upgrade at [claude.com](https://claude.com).
- A **GitHub account**. Free is fine. If you do not have one, create it at
  [github.com](https://github.com). Pick a username, confirm your email,
  and you are done.

You do **not** need to install Git, Python, Node, or any other tool. Claude
Code runs in a cloud machine that Anthropic manages.

## Step 1: Sign in to Claude Code on the web

1. Open [claude.ai/code](https://claude.ai/code) in your browser.
2. Sign in with your Claude account (the same one you use for chat).
3. You will land on the Claude Code home screen. It looks like a chat box
   with a repository picker just below it.

If the page only shows a "Sign in with GitHub" button, continue to step 2.

## Step 2: Connect your GitHub account

The first time you open Claude Code on the web, it will ask you to connect
GitHub. This is what lets Claude read and write code in your repositories.

1. Click the prompt to **connect GitHub**.
2. GitHub opens in a new tab and asks you to install the **Claude GitHub
   App**.
3. Choose which repositories Claude can see:
   - **All repositories** is the simplest option for a workshop. You can
     change this later.
   - **Only select repositories** if you prefer to grant access one at a
     time. You can come back and add more whenever you want.
4. Click **Install** (or **Install & Authorize**) and confirm with your
   GitHub password if asked.
5. You will be redirected back to Claude Code.

Claude Code will then ask you to **create a cloud environment**. This is
the virtual machine your sessions run in.

- **Name**: anything you like, for example `workshop`.
- **Network access**: leave it on the default, `Trusted`. This lets Claude
  install packages from common registries while blocking the wider
  internet.
- **Environment variables** and **Setup script**: leave both empty for
  now. You will not need them today.

Click **Create environment**. You only do this once.

## Step 3a: Connect to a repository you already have

If you already have a GitHub repository you want to work in:

1. On the Claude Code home screen, click the **repository selector** below
   the chat input.
2. Pick your repository from the list. If you do not see it, open
   [github.com/settings/installations](https://github.com/settings/installations),
   find **Claude**, click **Configure**, and add the repository under
   **Repository access**.
3. Pick a branch. The default is usually `main`. For a workshop, working
   on `main` is fine; for real projects you may want to pick a feature
   branch.
4. In the chat box, describe what you want Claude to do, for example:

   > Add a `README.md` that explains what this repository is for.

5. Press Enter. Claude clones the repo into its cloud machine, makes the
   change, and pushes the result back to GitHub on a new branch. When it
   is finished, you can review the diff and create a pull request right
   from the same page.

That is the full loop: describe, review, merge.

## Step 3b: Create a brand new repository from scratch

If you do not have a repository yet, you create one on GitHub first and
then point Claude Code at it.

### Create the repository on GitHub

1. In a new browser tab, go to
   [github.com/new](https://github.com/new).
2. **Owner**: leave this on your own account (or pick your organisation).
3. **Repository name**: a short, lowercase name with dashes between words,
   for example `ai-bridges-sandbox`.
4. **Description**: one line about what the repo is for. Optional.
5. **Public or Private**: either works. Public is fine for workshop
   exercises.
6. Tick **Add a README file**. This is important: Claude Code needs the
   repository to have at least one file (and therefore one branch) before
   it can start working in it. The README gives you both.
7. Leave the other defaults as they are and click **Create repository**.

You now have an empty-ish repository at
`github.com/<your-username>/<repo-name>`.

### Give Claude access to the new repository

If during Step 2 you granted access to **all repositories**, Claude can
already see it. Skip to the next part.

If you granted access to **only select repositories**:

1. Go to
   [github.com/settings/installations](https://github.com/settings/installations).
2. Find **Claude** in the list and click **Configure**.
3. Under **Repository access**, add the repository you just created.
4. Click **Save**.

### Start working in it from Claude Code

1. Go back to [claude.ai/code](https://claude.ai/code).
2. Click the **repository selector** below the chat input and pick your
   new repository. You may need to refresh the page if it does not show
   up immediately.
3. Type a first task in the chat box, for example:

   > Set up this repository as a Python project with a simple
   > "hello world" script and a short README that explains how to run it.

4. Press Enter and let Claude work. When it is done, review the changes,
   leave comments on any lines you want to adjust, and click **Create
   PR** to open a pull request on GitHub.

## Tips

- **Be specific.** "Add a function that fetches the first 10 objects from
  the V&A API and prints their titles" works better than "use the V&A
  API".
- **Each task gets its own branch.** You can start a second task before
  the first one finishes; they will not interfere with each other.
- **Closing the browser tab does not stop Claude.** The session keeps
  running in the cloud. Open
  [claude.ai/code](https://claude.ai/code) again to pick up where you
  left off.
- **Look at the diff before merging.** Claude is fast and usually right,
  but you are still the one merging code into your repository. Treat its
  output the way you would treat a pull request from a colleague.

## If something goes wrong

- **No repositories show up after connecting GitHub.** Open
  [github.com/settings/installations](https://github.com/settings/installations),
  click **Configure** on **Claude**, and make sure your repository is
  listed under **Repository access**.
- **"Not available for the selected organization".** Your Claude plan
  does not currently include Claude Code on the web, or your enterprise
  admin has not enabled it. Check your plan at
  [claude.com](https://claude.com).
- **Claude cannot find a branch to work on.** Your repository is
  completely empty. Add a `README.md` on GitHub (or tick "Add a README
  file" when creating the repo) so there is at least one commit on
  `main`.

## Where to go next

- Official quickstart:
  [Get started with Claude Code on the web](https://code.claude.com/docs/en/web-quickstart).
- Full reference:
  [Use Claude Code on the web](https://code.claude.com/docs/en/claude-code-on-the-web).
- For workshop participants: the exercises in this repository assume you
  have completed the three steps above.
