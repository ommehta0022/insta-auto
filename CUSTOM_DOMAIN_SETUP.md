# Custom Domain Setup - massaari.com on Render

## Complete Guide to Connect massaari.com to Your Render Site

---

## Part 1: Add Domain in Render Dashboard

### Step 1: Go to Your Render Site
1. Login to **https://dashboard.render.com**
2. Click on your **massaari** static site
3. Go to **"Settings"** tab

### Step 2: Add Custom Domain
1. Scroll down to **"Custom Domains"** section
2. Click **"+ Add Custom Domain"**
3. Enter: `massaari.com`
4. Click **"Save"**
5. Repeat for: `www.massaari.com`
6. Click **"Save"** again

### Step 3: Note the DNS Records
Render will show you DNS records to add. They will look like:

**For massaari.com (root domain):**
```
Type: A
Name: @
Value: 216.24.57.1
```

**For www.massaari.com:**
```
Type: CNAME
Name: www
Value: massaari.onrender.com
```

⚠️ **IMPORTANT:** Copy these exact values from your Render dashboard!

---

## Part 2: Configure DNS at Your Domain Registrar

### Where Did You Buy massaari.com?

Choose your registrar below:

---

### 🔹 **Option A: GoDaddy**

1. Go to **https://dcc.godaddy.com/manage/MASSAARI.COM/dns**
2. Click **"DNS"** → **"Manage Zones"**
3. Find **"DNS Records"** section

**Add A Record:**
- Click **"Add"**
- Type: **A**
- Name: **@**
- Value/Points to: **216.24.57.1** (from Render)
- TTL: **1 Hour** (or 3600 seconds)
- Click **"Save"**

**Add CNAME Record:**
- Click **"Add"**
- Type: **CNAME**
- Name: **www**
- Value/Points to: **massaari.onrender.com** (from Render)
- TTL: **1 Hour**
- Click **"Save"**

---

### 🔹 **Option B: Namecheap**

1. Go to **https://ap.www.namecheap.com**
2. Click **"Domain List"**
3. Find **massaari.com** → Click **"Manage"**
4. Go to **"Advanced DNS"** tab

**Add A Record:**
- Click **"Add New Record"**
- Type: **A Record**
- Host: **@**
- Value: **216.24.57.1** (from Render)
- TTL: **Automatic**
- Click **"Save"** (green checkmark)

**Add CNAME Record:**
- Click **"Add New Record"**
- Type: **CNAME Record**
- Host: **www**
- Target: **massaari.onrender.com** (from Render)
- TTL: **Automatic**
- Click **"Save"**

---

### 🔹 **Option C: Cloudflare**

1. Go to **https://dash.cloudflare.com**
2. Select **massaari.com** domain
3. Click **"DNS"** tab

**Add A Record:**
- Click **"Add record"**
- Type: **A**
- Name: **@**
- IPv4 address: **216.24.57.1** (from Render)
- Proxy status: **DNS only** (gray cloud) ⚠️ IMPORTANT
- TTL: **Auto**
- Click **"Save"**

**Add CNAME Record:**
- Click **"Add record"**
- Type: **CNAME**
- Name: **www**
- Target: **massaari.onrender.com** (from Render)
- Proxy status: **DNS only** (gray cloud) ⚠️ IMPORTANT
- TTL: **Auto**
- Click **"Save"**

⚠️ **Cloudflare Note:** Keep proxy OFF (gray cloud) initially. Enable after SSL is active.

---

### 🔹 **Option D: Google Domains / Squarespace Domains**

1. Go to **https://domains.google.com** or **https://domains.squarespace.com**
2. Click on **massaari.com**
3. Click **"DNS"** in the left menu

**Add A Record:**
- Scroll to **"Custom resource records"**
- Host name: **@**
- Type: **A**
- TTL: **3600**
- Data: **216.24.57.1** (from Render)
- Click **"Add"**

**Add CNAME Record:**
- Host name: **www**
- Type: **CNAME**
- TTL: **3600**
- Data: **massaari.onrender.com** (from Render)
- Click **"Add"**

---

### 🔹 **Option E: Other Registrars (General Steps)**

1. Login to your domain registrar
2. Find DNS Management / DNS Settings / Name Servers
3. Add the following records:

**A Record:**
```
Type: A
Host/Name: @ (or leave blank for root)
Value/Points to: 216.24.57.1
TTL: 3600 (1 hour)
```

**CNAME Record:**
```
Type: CNAME
Host/Name: www
Value/Points to: massaari.onrender.com
TTL: 3600 (1 hour)
```

---

## Part 3: Verify DNS Configuration

### Method 1: Online DNS Checker
1. Go to **https://dnschecker.org**
2. Enter: `massaari.com`
3. Select: **A Record**
4. Click **"Search"**
5. Wait for green checkmarks worldwide (may take time)

Repeat for `www.massaari.com` with CNAME type

### Method 2: Command Line (Windows)
```powershell
# Check A record
nslookup massaari.com

# Check CNAME record
nslookup www.massaari.com
```

Should show:
- `massaari.com` → `216.24.57.1`
- `www.massaari.com` → `massaari.onrender.com`

---

## Part 4: Enable SSL Certificate (Automatic)

### In Render Dashboard:
1. Go to your site → **"Settings"**
2. Scroll to **"Custom Domains"**
3. Wait for status to change:
   - ❌ **"Verifying"** → DNS not propagated yet (wait)
   - ✅ **"Verified"** → DNS working!
4. SSL certificate is automatically provisioned (2-5 minutes)
5. Status changes to: ✅ **"Verified"** with 🔒 HTTPS

---

## Timeline & Propagation

| Step | Time |
|------|------|
| DNS propagation | 5 minutes - 48 hours (usually 30 min) |
| SSL certificate | 2-5 minutes after DNS verified |
| Full HTTPS | 30 minutes - 2 hours total |

**Tip:** Clear browser cache or use incognito mode when testing

---

## Testing Your Domain

### After DNS Propagation:
1. Visit: **http://massaari.com** (should redirect to HTTPS)
2. Visit: **https://massaari.com** (should show your site with 🔒)
3. Visit: **https://www.massaari.com** (should also work)

### If Not Working:
- Check DNS records are correct
- Wait longer (DNS can take up to 48 hours)
- Use incognito mode / clear cache
- Check Render dashboard for status

---

## Common Issues & Solutions

### Issue 1: "Domain not verified"
**Solution:** DNS hasn't propagated yet. Wait 30-60 minutes and refresh Render dashboard.

### Issue 2: "SSL certificate pending"
**Solution:** Wait 5-10 minutes after DNS verification. Render auto-provisions SSL.

### Issue 3: "This site can't be reached"
**Solution:** DNS records incorrect. Double-check A and CNAME records match Render values.

### Issue 4: "Not Secure" warning
**Solution:** SSL still provisioning. Wait a few more minutes. Force HTTPS in browser.

### Issue 5: Works on www but not root (or vice versa)
**Solution:** Add both A record (@) AND CNAME record (www) as shown above.

---

## Final Configuration Summary

Once complete, you should have:

✅ **DNS Records Set:**
- A Record: `@` → `216.24.57.1`
- CNAME: `www` → `massaari.onrender.com`

✅ **Render Dashboard:**
- Custom domain: `massaari.com` ✅ Verified 🔒
- Custom domain: `www.massaari.com` ✅ Verified 🔒

✅ **Live Site:**
- `https://massaari.com` → Works ✅
- `https://www.massaari.com` → Works ✅
- Auto HTTPS redirect → Active ✅
- SSL Certificate → Valid 🔒

---

## Need Help?

### Render Support:
- Documentation: https://render.com/docs/custom-domains
- Community: https://community.render.com

### DNS Propagation Checker:
- https://dnschecker.org
- https://www.whatsmydns.net

### Your Configuration:
- **Repository:** https://github.com/ommehta0022/insta-auto
- **Render Dashboard:** https://dashboard.render.com
- **Domain:** massaari.com
- **Target:** massaari.onrender.com (or your site name)

---

## Quick Reference Card

```
Domain: massaari.com
Registrar: [Your registrar name]
Render Site: massaari

DNS Records to Add:
┌─────────┬──────┬────────────────────────┐
│ Type    │ Name │ Value                  │
├─────────┼──────┼────────────────────────┤
│ A       │ @    │ 216.24.57.1           │
│ CNAME   │ www  │ massaari.onrender.com  │
└─────────┴──────┴────────────────────────┘

Wait: 30-60 minutes for DNS
Then: SSL auto-provisions in 5 minutes
Result: https://massaari.com LIVE! 🚀
```

---

**That's it! Your massaari.com domain will be live on Render with automatic HTTPS!** 🎉
