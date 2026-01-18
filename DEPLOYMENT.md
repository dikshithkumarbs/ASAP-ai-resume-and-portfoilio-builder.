# Deployment Guide for AI Resume & Portfolio Builder

This guide delineates the steps to deploy the AI Resume & Portfolio Builder application. Since this application uses a Node.js backend to securely proxy API requests to Google Gemini and Hugging Face, it requires a hosting service that supports Node.js (not just static file hosting like GitHub Pages).

## Prerequisites

- **GitHub Account**: To host your code.
- **Vercel or Render Account**: For hosting the application.
- **API Keys**: Google Gemini API Key and Hugging Face API Key.

## Option 1: Deploy to Vercel (Recommended)

Vercel is excellent for frontend projects with serverless backends.

1.  **Push to GitHub**: Ensure your code is pushed to your GitHub repository (you should have already done this step).
2.  **Login to Vercel**: Go to [vercel.com](https://vercel.com) and log in with GitHub.
3.  **Add New Project**:
    *   Click "Add New..." -> "Project".
    *   Select your `Edunet-internship` repository.
    *   Click "Import".
4.  **Configure Project**:
    *   **Framework Preset**: Select "Other" (or let it auto-detect).
    *   **Build Command**: Leave empty (unless you have a build script).
    *   **Output Directory**: `.` (root) or leave default.
    *   **Install Command**: `npm install`.
5.  **Environment Variables**:
    *   Expand the "Environment Variables" section.
    *   Add `GEMINI_API_KEY` with your actual key value.
    *   Add `HF_API_KEY` with your actual key value.
6.  **Deploy**: Click "Deploy".
7.  **Server Function**: Since this uses `server.js` as an Express app, a `vercel.json` configuration file has been included in the repository to tell Vercel to treat `server.js` as a serverless function.

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
