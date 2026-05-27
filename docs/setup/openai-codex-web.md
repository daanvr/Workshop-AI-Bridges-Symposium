# Set up OpenAI Codex in the browser

A short, beginner friendly walkthrough for using **OpenAI Codex on the
web**, the cloud version of OpenAI's coding agent. You do not install
anything on your computer. Everything happens in your browser, connected
to a **GitHub** repository.

By the end of this guide you will be able to:

1. Open Codex in your browser.
2. Connect it to GitHub.
3. Either create a brand new repository and start working in it, or
   connect Codex to a repository you already have.

If a step looks different in real life, the user interface may have
changed slightly since this guide was written (May 2026). The overall
flow is the same.

## What you need before starting

You need three things:

- A modern web browser (Chrome, Edge, Firefox or Safari).
- A **ChatGPT account** with a paid plan: **Plus, Pro, Business, Edu,
  or Enterprise**. Codex is not available on the free ChatGPT plan.
  Sign up or upgrade at [chatgpt.com](https://chatgpt.com).
- A **GitHub account**. Free is fine. If you do not have one, create it
  at [github.com](https://github.com).

You do **not** need to install Git, Python, Node, or any other tool.
Codex on the web runs in a cloud machine that OpenAI manages.

If you are on an Enterprise plan, your workspace admin may need to
enable Codex first. If so, ask whoever manages your ChatGPT workspace.

## Step 1: Open Codex in your browser

1. Go to [chatgpt.com/codex](https://chatgpt.com/codex).
2. Sign in with your ChatGPT account if you are not already signed in.

You will land on the Codex web interface.

## Step 2: Connect your GitHub account

The first time you open Codex on the web, it will ask you to connect
GitHub. This is what lets Codex read and write code in your
repositories.

1. Click the prompt to **connect GitHub**.
2. GitHub opens in a new tab and asks you to install the OpenAI Codex
   (or ChatGPT) GitHub app.
3. Choose which repositories Codex can see:
   - **All repositories** is the simplest option for a workshop. You
     can change this later.
   - **Only select repositories** if you prefer to grant access one at
     a time.
4. Click **Install** (or **Install & Authorize**) and confirm with your
   GitHub password if asked.
5. You will be redirected back to Codex.

Codex on the web works with **environments**: small descriptions of
which repository to clone and what setup steps to run. The first time
you start a task, Codex offers to create an environment for the
repository you pick. For a first session, accept the defaults.

## Step 3a: Connect Codex to a repository you already have

If you already have a GitHub repository you want to work in:

1. On the Codex web page, click the **repository selector** near the
   prompt input.
2. Pick your repository from the list. If it is missing, go to
   [github.com/settings/installations](https://github.com/settings/installations),
   find the OpenAI Codex app, click **Configure**, and add the
   repository under **Repository access**.
3. Choose a branch. The default branch (usually `main`) is selected for
   you.
4. Type a clear, specific task in the prompt box, for example:

   > Add a `README.md` that explains what this repository is for.

5. Press Enter. Codex clones the repo into its cloud machine, makes the
   change, and pushes a branch back to GitHub.
6. When Codex is done, review the diff. You can open it as a pull
   request directly from the Codex interface, or keep talking to Codex
   to refine the work before opening the PR.

## Step 3b: Create a brand new repository from scratch

If you do not have a repository yet, you create one on GitHub first and
then point Codex at it.

### Create the repository on GitHub

1. In a new browser tab, go to
   [github.com/new](https://github.com/new).
2. **Owner**: leave this on your own account.
3. **Repository name**: a short, lowercase name with dashes between
   words, for example `ai-bridges-sandbox`.
4. **Description**: one line about what the repo is for. Optional.
5. **Public or Private**: either works.
6. Tick **Add a README file**. Codex needs the repository to have at
   least one file (and therefore one branch) before it can start
   working in it.
7. Leave the other defaults and click **Create repository**.

### Give Codex access to the new repository

If during Step 2 you granted access to **all repositories**, Codex can
already see it. Skip to the next part.

If you granted access to **only select repositories**:

1. Go to
   [github.com/settings/installations](https://github.com/settings/installations).
2. Find the OpenAI Codex app in the list and click **Configure**.
3. Under **Repository access**, add the repository you just created.
4. Click **Save**.

### Start working in it from Codex

1. Go back to [chatgpt.com/codex](https://chatgpt.com/codex).
2. Click the **repository selector** and pick your new repository. You
   may need to refresh the page if it does not show up immediately.
3. If Codex prompts you to create an environment for this repository,
   accept the defaults.
4. Type a first task in the prompt box, for example:

   > Set up this repository as a Python project with a simple
   > "hello world" script and a short README that explains how to run it.

5. Press Enter. When Codex is done, review the diff and open a pull
   request from the Codex interface to merge the work into your repo
   on GitHub.

## Tips

- **Be specific.** "Add a function that fetches the first 10 objects
  from the V&A API and prints their titles" works better than "use the
  V&A API".
- **Tasks run in the background.** You can close the tab and come back;
  Codex keeps working in the cloud.
- **Tag Codex from GitHub.** Once Codex is connected, you can also
  trigger it from a GitHub issue or pull request by mentioning
  `@codex`, for example `@codex review` on a PR or `@codex` plus a
  description on an issue. The session shows up in your Codex web
  inbox.
- **Add an `AGENTS.md` file.** Codex reads a file called `AGENTS.md` in
  the root of your repository to learn project conventions. Keep it
  short and up to date.
- **Treat the pull request like a real one.** Codex is fast and usually
  right, but you are the one merging code. Review the diff the same
  way you would review a colleague's PR.

## If something goes wrong

- **No repositories show up after connecting GitHub.** Open
  [github.com/settings/installations](https://github.com/settings/installations),
  click **Configure** on the OpenAI Codex app, and make sure your
  repository is listed under **Repository access**.
- **"Codex is not available on this plan".** You are on the free
  ChatGPT plan, or your Enterprise admin has not enabled Codex. Check
  your plan at [chatgpt.com](https://chatgpt.com) or ask your admin.
- **Codex cannot find a branch to work on.** Your repository is
  completely empty. Add a `README.md` on GitHub (or tick "Add a README
  file" when creating the repo) so there is at least one commit on the
  default branch.

## Where to go next

- Official Codex on the web overview:
  [Codex web](https://developers.openai.com/codex/cloud).
- Quickstart across all surfaces (we are using the **Cloud** option):
  [Codex Quickstart](https://developers.openai.com/codex/quickstart).
- GitHub integration details:
  [Code review in GitHub](https://developers.openai.com/codex/integrations/github).
