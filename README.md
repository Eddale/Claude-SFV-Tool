# BlackBelt Video Script Creator - Deployment Guide

## What You Have

Three files ready to deploy to Vercel:

1. **blackbelt-video-creator.html** - Your front-end tool
2. **api/claude.js** - Backend proxy that keeps your API key secure
3. **vercel.json** - Configuration for routing

## Deployment Steps

### 1. Sign Up for Vercel
- Go to vercel.com
- Click "Sign Up"
- Use GitHub, GitLab, or email (GitHub is easiest)

### 2. Get Your Anthropic API Key
- Go to console.anthropic.com
- Navigate to API Keys
- Create a new key
- Copy it (you'll need it in step 4)

### 3. Deploy to Vercel

**Option A - Drag and Drop (Easiest):**
1. In Vercel dashboard, click "Add New Project"
2. Drag all three files/folders into the upload area
3. Click "Deploy"

**Option B - GitHub (More Professional):**
1. Create a new GitHub repo
2. Upload these three files
3. In Vercel, click "Import Project"
4. Connect your GitHub repo
5. Click "Deploy"

### 4. Add Your API Key as Environment Variable

CRITICAL STEP - Without this, the tool won't work:

1. In your Vercel project dashboard, go to "Settings"
2. Click "Environment Variables"
3. Add a new variable:
   - Name: `ANTHROPIC_API_KEY`
   - Value: [paste your API key from step 2]
4. Click "Save"
5. Go to "Deployments" tab
6. Click the three dots on your latest deployment
7. Click "Redeploy" (this makes the env var take effect)

### 5. Test It

Once deployment finishes (takes ~30 seconds):
- Click the deployment URL Vercel gives you
- Try uploading an article
- Make sure Claude responds

### 6. Embed in WordPress

Once it's working, you can iframe it into your member portal:

```html
<iframe 
  src="https://your-project-name.vercel.app" 
  width="100%" 
  height="800px" 
  frameborder="0"
  allow="clipboard-write"
></iframe>
```

## File Structure

```
your-project/
├── blackbelt-video-creator.html  (front-end)
├── api/
│   └── claude.js                 (backend proxy)
└── vercel.json                   (config)
```

## Security Notes

- Your API key lives in Vercel's environment variables (server-side only)
- Never expose your API key in the front-end HTML
- The backend proxy (api/claude.js) is what actually calls Claude
- Members never see your API key

## Troubleshooting

**Tool loads but doesn't respond:**
- Check you added the `ANTHROPIC_API_KEY` environment variable
- Make sure you redeployed after adding the env var

**"Method not allowed" error:**
- The API endpoint only accepts POST requests (this is correct)
- If you see this when using the tool, something's wrong with routing

**CORS errors:**
- Shouldn't happen with this setup, but if they do, the api/claude.js file handles it

## Cost Estimate

With 200 sessions/day:
- Vercel: Free (well under limits)
- Anthropic API: Depends on usage, but roughly $10-30/month for this volume

## Next Steps

1. Test thoroughly before sharing with members
2. Consider adding usage tracking
3. Maybe add a simple member authentication layer
4. Monitor API costs in Anthropic console

---

Questions? The setup is dead simple. If something's not working, 99% chance it's the environment variable step.
