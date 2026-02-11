# Manager Message Opt-Out

A simple mobile-friendly form for managers to opt out of receiving manager messages. Managers scan a QR code, enter their name and phone number, and submit. The data goes straight to a Google Sheet.

```
[QR Code] → [GitHub Pages form] → [Google Apps Script] → [Google Sheet]
```

## Setup

### 1. Create the Google Sheet

1. Go to [Google Sheets](https://sheets.google.com) and create a new spreadsheet
2. Name it **"Manager Opt-Outs"** (or whatever you prefer)
3. Go to **Extensions > Apps Script**
4. Delete any default code in the editor
5. Copy the contents of `apps-script.js` from this repo and paste it in
6. Click **Deploy > New deployment**
   - Click the gear icon next to "Select type" and choose **Web app**
   - **Execute as:** Me
   - **Who has access:** Anyone
7. Click **Deploy**
8. Authorize the script when prompted (click through the "unsafe" warning — it's your own script)
9. Copy the **Web App URL** — you'll need it in the next step

### 2. Configure the Form

Open `index.html` and find this line near the bottom:

```js
const SCRIPT_URL = 'YOUR_GOOGLE_APPS_SCRIPT_URL_HERE';
```

Replace `YOUR_GOOGLE_APPS_SCRIPT_URL_HERE` with the Web App URL from step 1.

### 3. Deploy to GitHub Pages

1. Create a new GitHub repo (e.g., `manager-opt-out`)
2. Push this code:
   ```bash
   git remote add origin https://github.com/YOUR_ORG/manager-opt-out.git
   git push -u origin main
   ```
3. Go to the repo's **Settings > Pages**
4. Under "Source," select **Deploy from a branch**
5. Branch: **main**, folder: **/ (root)**
6. Click **Save**
7. Your form will be live at: `https://YOUR_ORG.github.io/manager-opt-out/`

### 4. Generate a QR Code

Generate a QR code pointing to your GitHub Pages URL. Options:

- [qr-code-generator.com](https://www.qr-code-generator.com/)
- [qrcode.tec-it.com](https://qrcode.tec-it.com/)
- Any other QR generator

Print the QR code or display it at the summit.

## Testing

1. Open `index.html` directly in a browser to check the form UI
2. After setting the `SCRIPT_URL`, submit a test entry
3. Verify the row appears in your Google Sheet
4. Test on a phone to confirm mobile layout
5. Scan the QR code from a phone to test the full flow

## How It Works

- The form collects a **name** and **phone number**
- On submit, it POSTs the data to a Google Apps Script web app
- The script appends a row to the Google Sheet (with duplicate checking)
- The sheet can be shared, filtered, and exported as needed

## Updating the Apps Script

If you need to change the script after initial deployment:

1. Open the Google Sheet > Extensions > Apps Script
2. Edit the code
3. Click **Deploy > Manage deployments**
4. Click the pencil icon on your deployment
5. Set version to **New version**
6. Click **Deploy**
