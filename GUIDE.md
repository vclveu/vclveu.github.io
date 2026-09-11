# VCLV site — setup & editing guide

This site is built with a tool called Eleventy. You will almost never see that —
day to day, you just edit plain text files, and GitHub builds and publishes the
site automatically every time you save a change.

## One-time setup

1. **Create a GitHub account** at github.com, if you don't have one already.
2. **Create a new repository.** Click the "+" in the top right → "New repository".
   Name it whatever you like (e.g. `vclv-site`). Keep it **Public**. Don't add a
   README, .gitignore, or license — leave those unchecked.
3. **Upload this project.** On the new repository's page, click "uploading an
   existing file" and drag in everything from this folder (including hidden
   folders like `.github` — if your file browser hides them, show hidden files
   first). Commit the upload.
4. **Turn on GitHub Pages.** In the repository, go to Settings → Pages. Under
   "Build and deployment", set Source to **GitHub Actions**. That's it — GitHub
   will now build the site automatically every time you save changes.
5. **Point your domain at it.** In Settings → Pages, under "Custom domain",
   enter `vclv.eu` and save. Then, with whoever you bought the domain from, add
   these DNS records for vclv.eu:
   - Four `A` records for `@` pointing to: `185.199.108.153`, `185.199.109.153`,
     `185.199.110.153`, `185.199.111.153`
   - One `CNAME` record for `www` pointing to `<your-github-username>.github.io`
   This can take anywhere from a few minutes to a day to take effect. Back in
   Settings → Pages, tick "Enforce HTTPS" once it's available.
6. Open the "Actions" tab of your repository to watch the first build run. Once
   it finishes with a green checkmark, the site is live.

## Adding a new project

1. In the repository, open the `src/projects` folder.
2. Click "Add file" → "Create new file".
3. Name it something short and URL-friendly, e.g. `new-project-name.md`.
4. Paste in this template and fill it in:

   ```
   ---
   layout: project.njk
   order: 8
   title: Your Project Title
   summary: One sentence describing the project, shown on the Projects grid.
   hero: /images/projects/new-project-name/hero.jpg
   ---
   Your project write-up goes here, in plain text. Leave a blank line
   between paragraphs.

   ## A subheading, if you want one

   More text.

   ![](/images/projects/new-project-name/img-1.jpg)
   ```

5. `order` controls where it appears in the grid — lower numbers come first.
   Give the new one a number higher than any existing project.
6. To add images: go to `src/images/projects`, create a new folder with the
   same name you used above (e.g. `new-project-name`), and upload your photos
   into it there (GitHub lets you drag and drop). Reference them in your
   Markdown as `/images/projects/new-project-name/whatever.jpg`.
7. Scroll down and click "Commit changes". Within a minute or two, the new
   project is live on the site — check the Actions tab if you want to watch
   it build.

To remove a project, delete its file from `src/projects` the same way.

## Editing the home page

Home page text lives in `src/index.njk` — the tagline, the Expertise table,
and the Products section. Open it, edit the text between the HTML tags
(leave the tags themselves alone), and commit.

## Editing contact links

Both are in `src/_includes/base.njk`, near the bottom, inside the `<footer>`
section — look for the YouTube and LinkedIn links.

## If something looks broken

Check the "Actions" tab — a red X means the last build failed, and clicking
into it shows what went wrong (usually a small typo in a file's front matter,
the `---`-fenced block at the top of a Markdown file). You can always undo a
change from a file's "History" in GitHub.
