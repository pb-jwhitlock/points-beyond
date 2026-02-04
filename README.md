# Points Beyond

Personal website for Points Beyond - IT Strategy & Enterprise Transformation Consulting.

Built with [Astro](https://astro.build).

---

## Prerequisites

Before you begin, you need to install Node.js on your Mac.

### Installing Node.js

1. **Install Homebrew** (if you don't have it):

   Open Terminal and run:
   ```bash
   /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
   ```

   Follow the on-screen instructions. After installation, you may need to run additional commands shown in the terminal to add Homebrew to your PATH.

2. **Install Node.js**:
   ```bash
   brew install node
   ```

3. **Verify installation**:
   ```bash
   node --version
   npm --version
   ```

   You should see version numbers for both commands.

---

## Getting Started

### Install Dependencies

Navigate to the project folder and install dependencies:

```bash
cd ~/points-beyond
npm install
```

### Run Locally

Start the development server to preview your site:

```bash
npm run dev
```

Open your browser to `http://localhost:4321/points-beyond/` to see your site.

Press `Ctrl + C` in the terminal to stop the server.

### Build for Production

To create a production build:

```bash
npm run build
```

This creates a `dist/` folder with your static site files.

---

## Setting Up GitHub

### 1. Create a GitHub Account

If you don't have one, go to [github.com](https://github.com) and sign up for a free account.

### 2. Create a New Repository

1. Log in to GitHub
2. Click the **+** icon in the top right corner
3. Select **New repository**
4. Fill in the details:
   - **Repository name**: `points-beyond`
   - **Description**: "Points Beyond - IT Strategy Consulting Website"
   - **Public** or **Private**: Choose Public (required for free GitHub Pages)
   - Do NOT check "Add a README file" (we already have one)
5. Click **Create repository**

### 3. Connect Your Local Project to GitHub

After creating the repository, GitHub will show you commands. Run these in your terminal:

```bash
cd ~/points-beyond

# Initialize git in your project (if not already done)
git init

# Add all files to git
git add .

# Create your first commit
git commit -m "Initial commit: Points Beyond website"

# Connect to your GitHub repository (replace YOUR_USERNAME with your GitHub username)
git remote add origin https://github.com/YOUR_USERNAME/points-beyond.git

# Push your code to GitHub
git branch -M main
git push -u origin main
```

**Note**: You may be prompted to log in to GitHub. If you haven't set up Git credentials:
- GitHub will open a browser window for authentication, OR
- You may need to create a Personal Access Token (see GitHub's documentation)

---

## Deploying to GitHub Pages

GitHub Pages lets you host your website for free directly from your repository.

### Step 1: Update the Astro Configuration

Before deploying, you need to update `astro.config.mjs` with your GitHub username:

```javascript
// @ts-check
import { defineConfig } from 'astro/config';

export default defineConfig({
  site: 'https://YOUR_USERNAME.github.io',
  base: '/points-beyond',
});
```

Replace `YOUR_USERNAME` with your actual GitHub username.

After making this change, commit and push:

```bash
git add astro.config.mjs
git commit -m "Update site URL for GitHub Pages"
git push
```

### Step 2: Create the GitHub Actions Workflow

GitHub Actions will automatically build and deploy your site whenever you push changes.

1. Create the workflow directory:
   ```bash
   mkdir -p .github/workflows
   ```

2. Create a file called `.github/workflows/deploy.yml` with this content:

```yaml
name: Deploy to GitHub Pages

on:
  push:
    branches: [main]
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Setup Node
        uses: actions/setup-node@v4
        with:
          node-version: "20"
          cache: npm

      - name: Install dependencies
        run: npm ci

      - name: Build Astro
        run: npm run build

      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: ./dist

  deploy:
    needs: build
    runs-on: ubuntu-latest
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

3. Commit and push the workflow:
   ```bash
   git add .github/workflows/deploy.yml
   git commit -m "Add GitHub Pages deployment workflow"
   git push
   ```

### Step 3: Enable GitHub Pages

1. Go to your repository on GitHub
2. Click **Settings** (tab at the top)
3. In the left sidebar, click **Pages**
4. Under **Source**, select **GitHub Actions**
5. Wait for the deployment to complete (check the **Actions** tab to see progress)

### Step 4: View Your Site

Once deployed, your site will be available at:

```
https://YOUR_USERNAME.github.io/points-beyond/
```

---

## Making Changes

### Editing Content

The main content files are in `src/pages/`:
- `index.astro` - Home page
- `about.astro` - About page
- `services.astro` - Services page
- `contact.astro` - Contact page

The site layout (header, footer, navigation) is in `src/layouts/Layout.astro`.

### Deploying Updates

After making changes:

```bash
# See what files changed
git status

# Add your changes
git add .

# Commit with a message describing what you changed
git commit -m "Update homepage content"

# Push to GitHub (this triggers automatic deployment)
git push
```

Your changes will be live within a few minutes. Check the **Actions** tab on GitHub to monitor deployment progress.

---

## Project Structure

```
points-beyond/
├── public/
│   └── favicon.svg          # Site favicon
├── src/
│   ├── layouts/
│   │   └── Layout.astro     # Main layout (header, footer, styles)
│   └── pages/
│       ├── index.astro      # Home page
│       ├── about.astro      # About page
│       ├── services.astro   # Services page
│       └── contact.astro    # Contact page
├── astro.config.mjs         # Astro configuration
├── package.json             # Project dependencies
└── tsconfig.json            # TypeScript configuration
```

---

## Troubleshooting

### "command not found: npm"
You need to install Node.js. See the Prerequisites section above.

### "Permission denied" errors
Try running the command with `sudo` or check your file permissions.

### GitHub Pages not updating
1. Check the **Actions** tab on GitHub for any failed deployments
2. Make sure GitHub Pages is set to use "GitHub Actions" as the source
3. Clear your browser cache and try again

### Site shows 404
1. Make sure the `base` in `astro.config.mjs` matches your repository name
2. Check that GitHub Pages is enabled in repository settings
3. Wait a few minutes for deployment to complete

---

## Useful Commands

| Command         | Action                                      |
|----------------|---------------------------------------------|
| `npm install`  | Install dependencies                        |
| `npm run dev`  | Start local dev server at localhost:4321    |
| `npm run build`| Build production site to `./dist/`          |
| `npm run preview`| Preview production build locally          |

---

## Resources

- [Astro Documentation](https://docs.astro.build)
- [GitHub Pages Documentation](https://docs.github.com/en/pages)
- [Git Basics](https://docs.github.com/en/get-started/using-git)
