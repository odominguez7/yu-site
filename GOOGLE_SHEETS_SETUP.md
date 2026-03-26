# Google Sheets Waitlist Setup (2 minutes)

## Step 1: Create the Sheet
1. Go to https://sheets.google.com and create a new spreadsheet
2. Name it "YU Shield Waitlist"
3. In Row 1, add headers: **Email** (A1) | **Timestamp** (B1)

## Step 2: Add the Script
1. In the sheet, go to **Extensions > Apps Script**
2. Delete everything in the editor and paste this:

```javascript
function doPost(e) {
  var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
  var data = JSON.parse(e.postData.contents);
  sheet.appendRow([data.email, data.timestamp]);
  return ContentService
    .createTextOutput(JSON.stringify({ status: 'ok' }))
    .setMimeType(ContentService.MimeType.JSON);
}
```

3. Click **Save** (Ctrl+S)

## Step 3: Deploy
1. Click **Deploy > New deployment**
2. Click the gear icon, select **Web app**
3. Set "Execute as" to **Me**
4. Set "Who has access" to **Anyone**
5. Click **Deploy**
6. Click **Authorize access**, pick your Google account, click "Advanced" > "Go to Untitled project" > Allow
7. **Copy the Web app URL**

## Step 4: Update the site
Replace `YOUR_GOOGLE_APPS_SCRIPT_URL` in index.html with the URL you copied.

Then push: `cd ~/Desktop/yu-site && git add -A && git commit -m "add sheets url" && git push`
