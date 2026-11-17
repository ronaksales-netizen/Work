# Operation Desk – Setup Guide

Files:
- `index.html` – dashboard (GitHub Pages par chalega, public repo)
- `Code.gs` – backend (Google Sheet ke Apps Script me paste hoga)

Bina setup ke bhi `index.html` khol ke test kar sakte ho: Demo mode, password `demo123`, data sirf usi browser me.

---

## Step 1 – Google Sheet + Apps Script
1. Google Drive me nayi Google Sheet banao, naam: **Operation Desk Data**.
2. Sheet me **Extensions → Apps Script** kholo.
3. Jo code pehle se hai use hata ke `Code.gs` ka poora code paste karo, Save.

## Step 2 – Private GitHub repo (data backup)
1. GitHub par naya repo: **operation-desk-data**, **Private** select karo, "Add a README" tick karo.
2. Token banao: GitHub → Settings → Developer settings → Personal access tokens → **Fine-grained tokens** → Generate new token
   - Repository access: **Only select repositories** → `operation-desk-data`
   - Permissions → Repository → **Contents: Read and write**
   - Token copy kar lo (ye kisi ko mat bhejna, chat me bhi nahi).

## Step 3 – Script properties
Apps Script me **Project Settings (gear icon) → Script properties → Add** ye 4 daalo:

| Property | Value |
|---|---|
| APP_PASSWORD | dashboard ka password (aap jo rakhna chaho) |
| GITHUB_TOKEN | Step 2 wala token |
| GITHUB_REPO | `ronaksales-netizen/operation-desk-data` (apna username/repo) |
| GITHUB_BRANCH | `main` |

## Step 4 – Test
1. Apps Script me upar function dropdown se **setup** choose karke **Run**. Permission maange to Allow.
2. Check karo: Sheet me **Registration** aur **History** tab ban gaye, aur GitHub repo me `data/registration.json` aa gaya.

## Step 5 – Web App deploy
1. **Deploy → New deployment** → type: **Web app**
   - Execute as: **Me**
   - Who has access: **Anyone**
2. Deploy → jo **Web app URL** mile (…/exec) copy karo.

## Step 6 – Dashboard GitHub par
1. `index.html` kholo, upar ye line dhundo aur URL paste karo:
   `const API_URL = "PASTE_URL_HERE";`
2. GitHub par naya **public** repo, jaise **operation-desk**, usme `index.html` upload.
3. Repo → Settings → Pages → Branch: **main**, folder **/ (root)** → Save.
4. 1–2 minute me link milega: `https://ronaksales-netizen.github.io/operation-desk/`

---

## Kaise kaam karta hai
- **Save / Edit / Delete** → Sheet ka Registration tab turant update + History tab me entry + GitHub me commit (usi time).
- **Reg. No** auto (REG-0001…). Delete ke baad bhi number dobara use nahi hota. Pattern badalna ho to `Code.gs` me `idPrefix`.
- **Purana data wapas chahiye?** GitHub `operation-desk-data` → `data/registration.json` → **History** me har change ka commit hai. Sheet ke History tab me bhi delete hua poora record likha rehta hai.
- GitHub backup fail ho jaye to bhi Sheet me save ho jata hai, screen par warning aati hai.
- **Password** ek baar daalne par us browser me yaad rehta hai, "Log out" se hat jata hai.

## Baad me changes
- `Code.gs` badla → **Deploy → Manage deployments → Edit (pencil) → Version: New version → Deploy**. URL same rehta hai.
- `index.html` badla → GitHub repo me file replace kar do.
- Naya tab → `index.html` ke `TABS` aur `Code.gs` ke `TABS` dono me same key se add hota hai (ye main kar dunga).
