# Setting Up a Custom Domain for GitHub Pages

Follow these steps to connect your custom domain (e.g., kedesigns.org) to your GitHub Pages site.

## Prerequisites
- A custom domain name (e.g., kedesigns.org, www.kedesigns.org)
- Access to your domain's DNS settings
- Your repository already set up with GitHub Pages

---

## Step 1: Enable GitHub Pages in Your Repository

1. Go to your repository on GitHub: `https://github.com/YOUR_USERNAME/KEDesignsWebsite`
2. Click on **Settings** (top menu)
3. Scroll down to **Pages** in the left sidebar
4. Under **Source**, select:
   - **Branch**: `main` (or `master`)
   - **Folder**: `/ (root)`
5. Click **Save**

---

## Step 2: Add Your Custom Domain

1. Still in **Settings** → **Pages**
2. Under **Custom domain**, enter your domain:
   - For root domain: `kedesigns.org`
   - For subdomain: `www.kedesigns.org`
   - Or both (you'll need to set up DNS for both)
3. Click **Save**
4. GitHub will automatically create a `CNAME` file in your repository

**Note:** If you want to use both `kedesigns.org` and `www.kedesigns.org`, you'll need to:
- Add the root domain first
- Then add the www subdomain
- Or manually create the CNAME file (see Step 3)

---

## Step 3: Create/Verify CNAME File (Optional but Recommended)

GitHub should create this automatically, but you can also create it manually:

1. In your repository, create a new file named `CNAME` (no extension)
2. Add your domain name inside:
   ```
   kedesigns.org
   ```
   Or for www:
   ```
   www.kedesigns.org
   ```
3. Commit and push the file

**Important:** The CNAME file should contain ONLY your domain name, nothing else.

---

## Step 4: Configure DNS Settings

### If Using Squarespace for Domain Management:

1. **Log into Squarespace**
   - Go to: https://www.squarespace.com/login
   - Navigate to your domain settings

2. **Access DNS Settings**
   - Go to **Settings** → **Domains**
   - Click on your domain (kedesigns.org)
   - Click on **DNS Settings** or **Advanced DNS**

3. **Add A Records for Root Domain** (kedesigns.org)
   
   You need to add 4 A records. In Squarespace:
   
   - Click **Add Record** or **+**
   - Select **A Record**
   - **Host**: `@` or leave blank (for root domain)
   - **Points to**: `185.199.108.153`
   - **TTL**: 3600 (or Auto)
   - Click **Save**
   
   Repeat for all 4 IP addresses:
   - `185.199.108.153`
   - `185.199.109.153`
   - `185.199.110.153`
   - `185.199.111.153`

4. **Add CNAME Record for www** (www.kedesigns.org) - Optional
   
   - Click **Add Record** or **+**
   - Select **CNAME Record**
   - **Host**: `www`
   - **Points to**: `YOUR_USERNAME.github.io` (replace with your GitHub username)
   - **TTL**: 3600 (or Auto)
   - Click **Save**

5. **Remove/Disable Squarespace Site Records** (Important!)
   
   If Squarespace has default A records pointing to their servers, you may need to:
   - Remove or disable any existing A records that point to Squarespace IPs
   - Keep only the GitHub Pages A records you just added
   - **Note**: This will disconnect your domain from Squarespace hosting (which is what you want for GitHub Pages)

6. **Save All Changes**

**Squarespace-Specific Notes:**
- Squarespace may show a warning about disconnecting from their hosting - this is expected
- The DNS changes in Squarespace can take a few minutes to propagate
- Make sure you're editing DNS, not website settings

---

### If Using Another Domain Registrar (GoDaddy, Namecheap, etc.):

1. Log into your domain registrar
2. Go to DNS Management / DNS Settings
3. Add or modify these **A records**:

   | Type | Name | Value | TTL |
   |------|------|-------|-----|
   | A | @ | 185.199.108.153 | 3600 |
   | A | @ | 185.199.109.153 | 3600 |
   | A | @ | 185.199.110.153 | 3600 |
   | A | @ | 185.199.111.153 | 3600 |

4. (Optional) Add **CNAME record** for www:

   | Type | Name | Value | TTL |
   |------|------|-------|-----|
   | CNAME | www | YOUR_USERNAME.github.io | 3600 |

5. Save the changes

---

## Step 5: Wait for DNS Propagation

DNS changes can take anywhere from a few minutes to 48 hours to propagate.

1. Check DNS propagation: https://www.whatsmydns.net/
2. Enter your domain and check if the A records are pointing to GitHub's IPs
3. Be patient - it usually takes 1-24 hours

---

## Step 6: Enable HTTPS (Enforce HTTPS)

1. Go back to GitHub repository → **Settings** → **Pages**
2. Wait until you see: "Your site is published at https://kedesigns.org"
3. Check the box: **Enforce HTTPS**
4. This enables free SSL certificate from Let's Encrypt

**Note:** You must wait for DNS to fully propagate before enabling HTTPS.

---

## Step 7: Verify It's Working

1. Visit your custom domain: `https://kedesigns.org`
2. Your GitHub Pages site should load
3. Check that HTTPS is working (padlock icon in browser)

---

## Troubleshooting

### Site Not Loading
- **Wait longer**: DNS can take up to 48 hours
- **Check DNS records**: Verify A records point to GitHub IPs
- **Clear browser cache**: Try incognito/private mode
- **Check CNAME file**: Make sure it exists and has correct domain

### HTTPS Not Working
- **Wait for DNS**: HTTPS can only be enabled after DNS propagates
- **Check GitHub Pages status**: Look for any warnings in Settings → Pages
- **Remove and re-add domain**: Sometimes removing and re-adding helps

### Both www and non-www
- If you want both to work, set up DNS for both
- GitHub will automatically redirect one to the other
- You can choose which is primary in GitHub Pages settings

### Common DNS Issues
- **Wrong IP addresses**: Make sure you're using current GitHub Pages IPs
- **TTL too high**: Lower TTL during setup (3600 seconds)
- **Cached DNS**: Your computer may have cached old DNS - wait or flush DNS
- **Squarespace warnings**: If Squarespace warns about disconnecting from hosting, that's expected - you're moving to GitHub Pages
- **Squarespace default records**: Make sure to remove/disable any Squarespace default A records that point to their servers

---

## Quick Reference: GitHub Pages IP Addresses

As of 2024, GitHub Pages uses these IP addresses:
- 185.199.108.153
- 185.199.109.153
- 185.199.110.153
- 185.199.111.153

**Always check GitHub's official documentation for current IPs:**
https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site

---

## Example: Complete Setup for kedesigns.org (Squarespace)

1. **GitHub Repository Settings:**
   - Custom domain: `kedesigns.org`
   - Enforce HTTPS: ✓ (after DNS propagates)

2. **Squarespace DNS Records:**
   
   **A Records (add 4 separate records):**
   - Host: `@` (or blank)
   - Points to: `185.199.108.153`
   - TTL: 3600
   
   - Host: `@` (or blank)
   - Points to: `185.199.109.153`
   - TTL: 3600
   
   - Host: `@` (or blank)
   - Points to: `185.199.110.153`
   - TTL: 3600
   
   - Host: `@` (or blank)
   - Points to: `185.199.111.153`
   - TTL: 3600
   
   **CNAME Record (optional for www):**
   - Host: `www`
   - Points to: `YOUR_USERNAME.github.io`
   - TTL: 3600

3. **CNAME File in Repository:**
   ```
   kedesigns.org
   ```

4. **Wait 1-24 hours** for DNS propagation

5. **Enable HTTPS** in GitHub Pages settings

**Important for Squarespace Users:**
- You may see a warning in Squarespace about disconnecting from their hosting - this is normal and expected
- Your domain will no longer point to Squarespace hosting, but will point to GitHub Pages
- You can still manage your domain through Squarespace, just the DNS records change

---

## Need Help?

- GitHub Pages Docs: https://docs.github.com/en/pages
- DNS Propagation Checker: https://www.whatsmydns.net/
- GitHub Support: https://support.github.com/

