# Set up Jules (Google's Gemini coding agent) in the browser

A short, beginner friendly walkthrough for using **Jules**, Google's
browser based coding agent powered by Gemini. You do not install anything
on your computer. Everything happens in your browser, connected to a
**GitHub** repository.

By the end of this guide you will be able to:

1. Sign in to Jules.
2. Connect it to GitHub.
3. Either create a brand new repository and start working in it, or
   connect Jules to a repository you already have.

If a step looks different in real life, the user interface may have
changed slightly since this guide was written (May 2026). The overall
flow is the same.

## What you need before starting

You need three things:

- A modern web browser (Chrome, Edge, Firefox or Safari).
- A **Google account** (the same one you use for Gmail, Drive, etc.). A
  free account works. Jules is in public beta and free to use during
  the beta, subject to usage limits.
- A **GitHub account**. Free is fine. If you do not have one, create it
  at [github.com](https://github.com).

You do **not** need to install Git, Python, Node, or any other tool.
Jules runs in a cloud virtual machine that Google manages.

## Step 1: Sign in to Jules

1. Open [jules.google.com](https://jules.google.com) in your browser.
2. Click **Sign in** and choose your Google account.
3. Accept the privacy notice (you only see this once).

You will land on the Jules home screen.

## Step 2: Connect your GitHub account

The first time you open Jules, it will ask you to connect GitHub. This
is what lets Jules read and write code in your repositories.

1. Click **Connect to GitHub account**.
2. GitHub opens in a new tab and asks you to install the Jules GitHub
   app.
3. Choose which repositories Jules can see:
   - **All repositories** is the simplest option for a workshop. You can
     change this later.
   - **Only select repositories** if you prefer to grant access one at a
     time.
4. Click **Install** (or **Install & Authorize**) and confirm with your
   GitHub password if asked.
5. You will be redirected back to Jules. If not, refresh the page.

Once connected, Jules shows a **repo selector** with the repositories
you gave it access to, and a prompt box where you can type tasks.

## Step 3a: Connect Jules to a repository you already have

If you already have a GitHub repository you want to work in:

1. On the Jules home screen, click the **repo selector**.
2. Pick your repository from the list. If it is missing, go to
   [github.com/settings/installations](https://github.com/settings/installations),
   find **Jules**, click **Configure**, and add the repository under
   **Repository access**.
3. Choose the branch you want Jules to work on. The default branch
   (usually `main`) is selected for you; leave it as is for a workshop.
4. (Optional) Tick the option to add environment setup scripts if your
   project needs specific dependencies installed. For a first task you
   can skip this.
5. Type a clear, specific prompt in the prompt box, for example:

   > Add a `README.md` that explains what this repository is for.

6. Click **Give me a plan**. Jules will think for a moment and show you
   a plan of what it intends to do.
7. Read the plan. If it looks right, approve it. Jules then makes the
   changes in its cloud machine and shows you a **diff** (a side by
   side view of what changed). When you accept, it pushes a branch and
   opens a pull request back to GitHub for you to review and merge.

## Step 3b: Create a brand new repository from scratch

If you do not have a repository yet, you create one on GitHub first and
then point Jules at it.

### Create the repository on GitHub

1. In a new browser tab, go to
   [github.com/new](https://github.com/new).
2. **Owner**: leave this on your own account.
3. **Repository name**: a short, lowercase name with dashes between
   words, for example `ai-bridges-sandbox`.
4. **Description**: one line about what the repo is for. Optional.
5. **Public or Private**: either works.
6. Tick **Add a README file**. This is important: Jules needs the
   repository to have at least one file (and therefore one branch)
   before it can start working in it.
7. Leave the other defaults and click **Create repository**.

### Give Jules access to the new repository

If during Step 2 you granted access to **all repositories**, Jules can
already see it. Skip to the next part.

If you granted access to **only select repositories**:

1. Go to
   [github.com/settings/installations](https://github.com/settings/installations).
2. Find **Jules** in the list and click **Configure**.
3. Under **Repository access**, add the repository you just created.
4. Click **Save**.

### Start working in it from Jules

1. Go back to [jules.google.com](https://jules.google.com).
2. Click the **repo selector** and pick your new repository. You may
   need to refresh the page if it does not show up immediately.
3. Type a first task in the prompt box, for example:

   > Set up this repository as a Python project with a simple
   > "hello world" script and a short README that explains how to run it.

4. Click **Give me a plan**, approve the plan, and let Jules work. When
   it is done, review the diff, accept it, and Jules will push a branch
   and create a pull request on GitHub.

## Tips

- **Be specific.** "Add a function that fetches the first 10 objects
  from the V&A API and prints their titles" works better than "use the
  V&A API".
- **Look at the plan before you let Jules code.** Jules shows its
  reasoning up front; that is your chance to redirect it cheaply.
- **You can step away.** Tasks run in the cloud, so you can close the
  tab and come back. Enable browser notifications when prompted to be
  pinged when Jules is done.
- **Add an `AGENTS.md` file.** Jules looks for a file called
  `AGENTS.md` in the root of the repository. You can use it to write
  short notes about your project that Jules should keep in mind.
- **Treat the pull request like a real one.** Jules is fast and usually
  right, but you are the one merging code into your repo. Review the
  diff the same way you would review a colleague's PR.

## If something goes wrong

- **No repositories show up after connecting GitHub.** Open
  [github.com/settings/installations](https://github.com/settings/installations),
  click **Configure** on **Jules**, and make sure your repository is
  listed under **Repository access**.
- **Jules cannot find a branch to work on.** Your repository is
  completely empty. Add a `README.md` on GitHub (or tick "Add a README
  file" when creating the repo) so there is at least one commit on the
  default branch.
- **You hit usage limits.** Jules is free during the public beta but
  has daily limits. Wait a few hours and try again, or split your task
  into smaller pieces.

## Where to go next

- Official quickstart: [Getting started with Jules](https://jules.google/docs/).
- Running tasks in depth:
  [Running a task with Jules](https://jules.google/docs/running-tasks/).
- A library of example prompts:
  [Jules Awesome Prompts](https://github.com/google-labs-code/jules-awesome-list).
