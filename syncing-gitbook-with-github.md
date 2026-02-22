# How I Set Up GitHub Sync for My GitBook Blog

If you've ever written something in GitBook and wished you could just open a terminal, write a Markdown file, `git push`, and have it automatically show up on your blog — this post is for you. That's exactly what I set up, and it's way cleaner than I expected.

Here's the full walkthrough of how I connected my [GitBook blog](https://bob.ltneighbor.net/) to a GitHub repo so I can write and publish from my laptop.

---

## Why Bother?

GitBook's editor is great, but I want my writing to live in a git repo. That means:

* Version history on every post
* Write in any editor (VS Code, Neovim, whatever)
* Push to publish — no browser required
* My content isn't locked inside a platform

The goal: **write Markdown locally → `git push` → blog updates automatically.**

---

## What You'll Need

* A [GitBook](https://gitbook.com/) account with an existing Space
* A [GitHub](https://github.com/) account
* The `gh` CLI or access to GitHub in a browser

---

## Step 1: Open the GitHub Sync Integration in GitBook

In GitBook, navigate to your **Space** (not the Docs Site — the Space level). Click **Integrations** in the left sidebar, then find **GitHub Sync** and click **Install**.

> ⚠️ Make sure you're in the Space settings, not the Docs Site settings. GitHub Sync only lives at the Space level.

---

## Step 2: Install the GitBook GitHub App

Click **Authenticate with GitHub**. GitBook will open a GitHub OAuth screen — authorize it.

After OAuth, you'll see the **Account** dropdown is still empty. That's because OAuth alone isn't enough — you also need to install the **GitBook GitHub App** on your GitHub account.

Click the **"Install the GitHub app"** link in the GitBook config. GitHub will ask you which repositories the app can access. Choose **All repositories** (simplest option), then click **Save**.

---

## Step 3: Re-Authorize GitBook

After installing the App, go back to GitBook and click the **Connected** button next to Authenticate. GitHub will prompt you to update GitBook's authorized permissions — click **Authorize GitBook.com**.

Now when you open the **Account** dropdown, you should see your GitHub username appear. Select it.

---

## Step 4: Create a GitHub Repo for Your Blog

If you don't have a dedicated repo yet, create one:

```bash
gh repo create your-username/blog --public --description "Blog synced with GitBook"
```

Then add an initial commit so it's not empty:

```bash
gh repo clone your-username/blog
cd blog
echo "# My Blog" > README.md
git add README.md && git commit -m "Initial commit" && git push
```

---

## Step 5: Select the Repo in GitBook

Back in the GitBook config, open the **Select repository** dropdown and choose your newly created `blog` repo.

> **Note:** If the repo doesn't appear immediately, it's a caching issue on GitBook's side — new repos can take a few minutes to show up. Give it a couple minutes and try again.

---

## Step 6: Choose Your Initial Sync Direction

GitBook asks: **which content wins on first sync?**

* **GitHub to GitBook** — imports GitHub content, replaces GitBook content
* **GitBook to GitHub** — exports GitBook content to GitHub, replaces repo content

Since my blog content already lived in GitBook, I chose **GitBook to GitHub**. This exported all my existing posts as Markdown files into the repo.

> If you're starting fresh with content in GitHub, pick the other direction.

Click **Sync**.

---

## The Result

After the sync, my `rftheisen/blog` repo was populated with all my blog posts as `.md` files, organized in folders, with a `SUMMARY.md` that acts as the table of contents:

```
SUMMARY.md
README.md
my-teaching-philosophy.md
amplify-your-learning-by-building-a-home-lab.md
educational-walkthroughs-and-reviews/
    hackthebox-netmon-walkthrough.md
    ai-learning-resources-for-beginners.md
...
```

---

## My Publishing Workflow Now

```bash
# Clone the repo once
git clone https://github.com/rftheisen/blog
cd blog

# Write a new post
touch my-new-post.md
# ... write in VS Code or any editor ...

# Add it to SUMMARY.md so GitBook knows where it lives
# Then push
git add .
git commit -m "Add new post: my-new-post"
git push
```

That's it. GitBook picks up the push automatically and publishes within seconds.

---

## Key Takeaways

* You need **both** GitHub OAuth **and** the GitBook GitHub App installed — OAuth alone won't work
* The sync is **truly bidirectional** — you can write in GitBook or GitHub and both stay in sync
* `SUMMARY.md` is the table of contents — any new post needs an entry there to appear in the navigation
* Images go in `.gitbook/assets/` and are referenced normally in Markdown

If you're a sysadmin or developer who lives in the terminal, this setup makes blogging feel a lot more like the rest of your workflow. Highly recommend.
