# Deployment Guide - Massaari.com on Render

## Automatic Deployment Setup

This guide will help you deploy Massaari.com to Render with automatic deployments from GitHub.

## Prerequisites

1. GitHub repository: `https://github.com/ommehta0022/insta-auto`
2. Render account (free): `https://render.com`

## Step-by-Step Deployment

### 1. Create Render Account
- Go to https://render.com
- Sign up with your GitHub account (ommehta0022)
- This allows Render to access your repositories

### 2. Deploy Static Site

1. **From Render Dashboard:**
   - Click "New +" button
   - Select "Static Site"

2. **Connect Repository:**
   - Choose "insta-auto" repository
   - Click "Connect"

3. **Configure Build Settings:**
   - **Name:** `massaari` (or any name you prefer)
   - **Branch:** `main`
   - **Build Command:** Leave empty (or use: `echo "Static site ready"`)
   - **Publish Directory:** `.` (current directory)

4. **Click "Create Static Site"**

### 3. Automatic Deployment (Already Configured!)

✅ **Auto-deploy is enabled by default on Render!**

Every time you push to the `main` branch on GitHub, Render will:
1. Detect the new commit
2. Automatically trigger a new deployment
3. Deploy your changes within 1-2 minutes

### 4. Custom Domain Setup (Optional)

To use your `massaari.com` domain:

1. **In Render Dashboard:**
   - Go to your static site
   - Click "Settings" tab
   - Scroll to "Custom Domain"
   - Click "Add Custom Domain"
   - Enter: `massaari.com` and `www.massaari.com`

2. **Update DNS Settings** (at your domain registrar):
   ```
   Type: A Record
   Name: @
   Value: [Render's IP - shown in dashboard]

   Type: CNAME
   Name: www
   Value: [your-site].onrender.com
   ```

3. **SSL Certificate:**
   - Render automatically provisions free SSL certificates
   - Your site will be available at `https://massaari.com`

## Configuration Files

### render.yaml
The `render.yaml` file in the repository configures:
- Static site hosting
- Cache headers for performance
- Routing rules

### Performance Optimizations
- **Cache Control:** CSS/assets cached for 1 year
- **HTML:** Cached for 1 hour (allows quick updates)
- **Gzip Compression:** Enabled automatically by Render
- **CDN:** Render uses global CDN for fast delivery

## Testing Deployment

After deployment, your site will be available at:
- **Render URL:** `https://massaari.onrender.com` (or your chosen name)
- **Custom Domain:** `https://massaari.com` (after DNS setup)

## Monitoring

### View Deployments:
1. Go to Render Dashboard
2. Click on your static site
3. See deployment history and logs

### Check Status:
- **Green:** Deployment successful
- **Building:** Deployment in progress
- **Failed:** Check logs for errors

## Making Updates

Simply push to GitHub:
```bash
git add .
git commit -m "Update content"
git push origin main
```

Render will automatically deploy within 1-2 minutes! ✅

## Rollback (if needed)

1. Go to Render Dashboard
2. Click "Deploys" tab
3. Find the working version
4. Click "Rollback to this deploy"

## Free Tier Limits

Render Free Tier includes:
- ✅ Unlimited static sites
- ✅ Automatic SSL certificates
- ✅ Global CDN
- ✅ Auto-deploy from GitHub
- ⚠️ Sites may spin down after inactivity (restarts in ~30 seconds)

For 24/7 uptime, upgrade to paid plan ($7/month)

## Support

- Render Documentation: https://render.com/docs/static-sites
- Render Community: https://community.render.com

## Quick Reference

- **Repository:** https://github.com/ommehta0022/insta-auto
- **Render Dashboard:** https://dashboard.render.com
- **Auto-Deploy:** ✅ Enabled by default
- **Deploy Time:** 1-2 minutes per update
