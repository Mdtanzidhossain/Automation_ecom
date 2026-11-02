# Publish only this showcase

1. Create a new **public** GitHub repository, for example
   `ecommerce-e2e-automation-case-study`.
2. Extract the showcase ZIP into a new folder, separate from the private project.
3. In GitHub, choose **Add file ? Upload files**. Upload the contents of this
   folder: README.md, the other Markdown files and the assets folder.
4. Commit the upload. The README automatically displays the screenshots.
5. Pin the repository from your GitHub profile's Customize your pins option.

Upload the extracted contents, not just the ZIP, so visitors can read the case
study and see images directly. No GitHub password or token is needed by anyone
preparing these files. You sign in to your own GitHub account for the upload.

For Git CLI, run these commands **inside the extracted showcase folder only**:

```bash
git init
git branch -M main
git add README.md WALKTHROUGH.md PUBLISHING.md NOTICE.md assets
git commit -m "Add e-commerce automation portfolio case study"
git remote add origin https://github.com/YOUR_USERNAME/YOUR_SHOWCASE_REPOSITORY.git
git push -u origin main
```

Replace both placeholders with your repository details. Use GitHub's normal
browser/credential-manager authentication. Do not run these commands at the
private project's root and do not copy its .git, source, env or reports folders.

The sample results are fictional UI fixtures. Keep the demo labels and captions
when publishing; they prevent confusion with real execution results.
