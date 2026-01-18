# Deployment Guide for AI Resume & Portfolio Builder

This guide delineates the steps to deploy the AI Resume & Portfolio Builder application. Since this application uses a Node.js backend to securely proxy API requests to Google Gemini and Hugging Face, it requires a hosting service that supports Node.js (not just static file hosting like GitHub Pages).

## Prerequisites

- **GitHub Account**: To host your code.
- **Vercel or Render Account**: For hosting the application.
- **API Keys**: Google Gemini API Key and Hugging Face API Key.

## Option 1: Deploy to Vercel (Recommended)

Vercel is the best platform for this project because it provides native support for both the static frontend and the Node.js backend (via serverless functions) with almost zero configuration.

### Phase 1: Preparation
1.  **Verify GitHub Repository**: Go to your GitHub repository (`https://github.com/dikshithkumarbs/Edunet-internship`) and ensure the latest code (including `vercel.json` and `server.js`) is there.
2.  **Get API Keys**: Have your `GEMINI_API_KEY` and `HF_API_KEY` ready.

### Phase 2: Create Project in Vercel
1.  **Log in**: Go to [vercel.com](https://vercel.com) and log in using your **GitHub** account.
2.  **New Project**: On your dashboard, click the white **"Add New..."** button on the top right and select **"Project"**.
3.  **Import Git Repository**:
    *   You will see a list of your GitHub repositories.
    *   Find `Edunet-internship` and click the blue **"Import"** button next to it.

### Phase 3: Configuration (Crucial Step)
You will now see the "Configure Project" screen.
1.  **Project Name**: You can leave this as `Edunet-internship` or change it to `ai-resume-builder`.
2.  **Framework Preset**: Vercel should detect this automatically. If not, select **"Other"**.
    *   *Note: Do NOT select "Create React App" or "Next.js" since this is a vanilla JS + Node app.*
3.  **Root Directory**: Leave this as `./` (default).
4.  **Build and Output Settings**:
    *   **Build Command**: Leave empty.
    *   **Output Directory**: Leave empty.
    *   **Install Command**: Ensure this is `npm install` (default).

### Phase 4: Environment Variables
**Do not skip this step.** The app will not work without these.
1.  Expand the **"Environment Variables"** dropdown section.
2.  **Add First Key**:
    *   **Key**: `GEMINI_API_KEY`
    *   **Value**: (Paste your actual Gemini API key starting with `AIza...`)
    *   Click **"Add"**.
3.  **Add Second Key**:
    *   **Key**: `HF_API_KEY`
    *   **Value**: (Paste your actual Hugging Face API key starting with `hf_...`)
    *   Click **"Add"**.

### Phase 5: Deploy
1.  Click the big blue **"Deploy"** button.
2.  **Wait**: Vercel will now:
    *   Clone your repo.
    *   Install dependencies (`npm install`).
    *   Detect the `vercel.json` configuration.
    *   Build the serverless functions.
3.  **Success**: You will see a "Congratulations!" screen with a screenshot of your app.
4.  **Click the preview image** or the "Visit" button to open your live application.

### Understanding `vercel.json`
We included a `vercel.json` file to tell Vercel how to handle your code:
*   It routes all API requests (`/api/...`) to `server.js`.
*   It serves `index.html`, `css/`, and `js/` as static files for fast loading.
*   This ensures your API keys stay hidden on the "server" side while your UI loads instantly.

### Troubleshooting Vercel Issues
*   **500/502 Error on Generation**: This usually means API keys are missing. Go to **Settings -> Environment Variables** in your Vercel project dashboard, check if keys are correct, then go to **Deployments** and "Redeploy".
*   **"Cannot find module"**: Ensure `package.json` includes all dependencies (`express`, `cors`, etc.) and that you ran `npm install` locally before pushing (so `package-lock.json` is correct).
*   **Styling Missing**: Check if the `css` folder is correctly uploaded to GitHub.


## Option 2: Deploy to Render

Render offers a simple "Web Service" option perfect for Node.js apps.

1.  **Login to Render**: Go to [render.com](https://render.com).
2.  **New Web Service**: Click "New +" -> "Web Service".
3.  **Connect GitHub**: Connect your GitHub account and select the `Edunet-internship` repository.
4.  **Configure Service**:
    *   **Name**: Choose a name (e.g., `ai-resume-builder`).
    *   **Region**: Select the one closest to you.
    *   **Branch**: `main`.
    *   **Runtime**: Node.js.
    *   **Build Command**: `npm install`.
    *   **Start Command**: `npm start`.
5.  **Environment Variables**:
    *   Scroll down to "Environment Variables".
    *   Add `GEMINI_API_KEY` and `HF_API_KEY`.
6.  **Create Web Service**: Click "Create Web Service".
7.  Render will build and deploy your app. Once finished, you will get a URL (e.g., `https://ai-resume-builder.onrender.com`).
