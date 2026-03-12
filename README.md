# Improve Your Sales Game — Phase 1: Lead Collection

A scaffolded digital card game for sales training, built as part of a randomized controlled trial studying the effects of DGBL on cognitive load, self-efficacy, and sales competency.

## Quick Start (Local)

1. Clone this repo
2. Open `index.html` in any browser — no server required

## Deploy to GitHub Pages

### Step 1: Create Repository
1. Go to [github.com/new](https://github.com/new)
2. Name it `sales-game` (or any name you prefer)
3. Set to **Public**
4. Click **Create repository**

### Step 2: Upload Files
1. Click **"uploading an existing file"** on the empty repo page
2. Drag and drop the entire contents of this folder:
   - `index.html`
   - `img/` folder (with all card images)
   - `README.md`
3. Click **Commit changes**

### Step 3: Enable GitHub Pages
1. Go to **Settings** → **Pages** (left sidebar)
2. Under **Source**, select **Deploy from a branch**
3. Branch: **main**, Folder: **/ (root)**
4. Click **Save**
5. Wait 1-2 minutes, then your game is live at:
   ```
   https://YOUR-USERNAME.github.io/sales-game/
   ```

## File Structure

```
sales-game/
├── index.html          # Phase 1 game (responsive, mobile-first)
├── img/
│   ├── card_01.jpg     # A Sudden Call (Prospecting)
│   ├── card_02.jpg     # The Deep Dive (Pre-approach)
│   ├── card_03.jpg     # Is this your problem? (Needs Analysis)
│   ├── card_04.jpg     # We have this...and this... (Presentation)
│   ├── card_05.jpg     # This is how it can help... (Presentation)
│   ├── card_06.jpg     # Lukewarm Reception (Handling Objections)
│   ├── card_07.jpg     # But I... (Handling Objections)
│   ├── card_08.jpg     # Looking Good? (Closing)
│   ├── card_09.jpg     # Let's sign this... (Closing)
│   └── card_10.jpg     # How are you doing? (Follow-up)
└── README.md
```

## Adding Data Logging for the RCT

The game has a built-in logging stub. To enable data collection:

### Option A: Google Sheets (Simplest)

1. Create a Google Sheet
2. Go to **Extensions → Apps Script**
3. Paste this script:

```javascript
function doPost(e) {
  var sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
  var data = JSON.parse(e.postData.contents);
  sheet.appendRow([
    data.timestamp,
    data.participantId,
    data.event,
    JSON.stringify(data)
  ]);
  return ContentService.createTextOutput("OK");
}
```

4. Deploy as **Web App** (Execute as: Me, Access: Anyone)
5. Copy the deployment URL
6. In `index.html`, find `LOG_ENDPOINT = ""` and paste your URL

### Option B: Firebase (More Robust)

See [Firebase Realtime Database docs](https://firebase.google.com/docs/database/web/start) for setup.

## Scaling to 50 Cards

To add the remaining 40 cards:

1. Add images to `img/` as `card_11.jpg` through `card_50.jpg`
2. In `index.html`, extend the `CARDS` array with new entries
3. Each card needs: `id`, `img`, `title`, `stage`, `emoji`, `text`
4. Optionally add `hint` for scaffolded cards (first N cards)

## Technical Notes

- **Mobile-first responsive**: 3 breakpoints (phone/tablet/desktop)
- **Touch-optimized**: 48px+ touch targets, no tap delay
- **Zero dependencies**: No framework, no build step, no server
- **Logs**: Participant ID, card classifications, response times, deck order
- **Accessibility**: WCAG touch targets, semantic HTML, alt text on images
