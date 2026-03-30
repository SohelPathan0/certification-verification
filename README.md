# certificate-verification
<img width="900" height="900" alt="image" src="https://github.com/user-attachments/assets/12899f15-63de-4100-89b0-b1de95cf3ac5" />


# 🎓 GitHub Copilot Dev Days | Mumbai — Certificate Verification

> A GitHub Pages-powered certificate verification system for **GitHub Copilot Dev Days Mumbai**, organised by **Microsoft Student Ambassador** and **Dear Azure — Azure India**.

---

## 👥 Organisers

| | Community Organisers | |
|---|---|---|
| <img width="50" height="50" alt="image" src="https://github.com/user-attachments/assets/87e63550-95d1-470c-ac36-cdfa3edd7f9f" /> | **Microsoft Student Ambassador** | Organizer |
| <img width="50" height="50" alt="image" src="https://github.com/user-attachments/assets/21baa34b-7627-466f-a9c3-bedc97dfd1e7" />| **Dear Azure — Azure India** | In Association With |

---

## 🌐 Live Verification Page

```
https://SohelPathan0.github.io/certificate-verification/
```

To verify a specific certificate directly:

```
https://SohelPathan0.github.io/certificate-verification/?id=GCDM-081
```

---

## 📁 Repository Structure

```
certificate-verification/
├── index.html        # Verification page (GitHub Pages entry point)
├── data.json         # Certificate registry with all participant records
└── README.md         # This file
```

---

## ⚙️ How It Works

```
Certificate (PDF / Image)
  ├── Unique Link  →  https://SohelPathan0.github.io/certificate-verification/?id=GCDM-081
  └── QR Code      →  encodes the same URL above
                              ↓
              Verification page loads
                              ↓
          Fetches data.json from GitHub
                              ↓
       Looks up participant by certificate ID
                              ↓
    ✅ Shows participant details  OR  ❌ Invalid certificate
```

When a participant opens their unique link or scans their QR code:

1. The page reads the `?id=` parameter from the URL
2. It fetches `data.json` from this repository
3. It looks up the certificate ID and displays the participant's details
4. If the ID is not found, it shows an error message

---

## 📋 data.json Format

All participant certificates are stored in `data.json` at the root of this repository.

```json
{
  "certificates": [
    {
      "id": "GCDM-001",
      "name": "Participant Name",
      "event": "GitHub Copilot Dev Days | Mumbai",
      "role": "Participant"
    }
  ]
}
```

| Field   | Description                                      |
|---------|--------------------------------------------------|
| `id`    | Unique certificate ID in format `GCDM-XXX`       |
| `name`  | Full name of the participant                     |
| `event` | Event name (same for all participants)           |
| `role`  | Role at the event (e.g. Participant, Speaker)    |

---

## 🔗 Adding a Verification Link to Certificates

Each participant gets a unique link in this format:

```
https://SohelPathan0.github.io/certificate-verification/?id=GCDM-XXX
```

Replace `XXX` with the participant's certificate number (e.g. `GCDM-001` through `GCDM-083`).

You can add this link to the certificate design as:
- A clickable URL printed at the bottom of the certificate
- A QR code placed in a corner (see QR Code section below)

---

## 📱 Generating QR Codes

Install the required library:

```bash
pip install qrcode[pil]
```

Run this script locally to generate one QR code per participant:

```python
import json, qrcode, os

with open('data.json') as f:
    data = json.load(f)

BASE_URL = "https://SohelPathan0.github.io/certificate-verification/?id="
os.makedirs('qrcodes', exist_ok=True)

for cert in data['certificates']:
    url = BASE_URL + cert['id']
    img = qrcode.make(url)
    img.save(f"qrcodes/{cert['id']}.png")
    print(f"✅ {cert['id']} → {cert['name']}")

print(f"\nGenerated {len(data['certificates'])} QR codes in /qrcodes folder.")
```

This creates a `qrcodes/` folder with individual PNG files named `GCDM-001.png`, `GCDM-002.png`, etc.

---

## 🚀 Deployment (GitHub Pages Setup)

### Step 1 — Enable GitHub Pages

1. Go to your repository on GitHub
2. Click **Settings** → **Pages**
3. Under **Branch**, select `main` and folder `/ (root)`
4. Click **Save**

Your verification page will be live at:
```
https://SohelPathan0.github.io/certificate-verification/
```

### Step 2 — Push your files

Make sure the following files are at the root of your `main` branch:

```bash
git add index.html data.json README.md
git commit -m "Add certificate verification page"
git push origin main
```

GitHub Pages will automatically deploy within a few minutes.

---

## ➕ Adding New Participants

1. Open `data.json`
2. Add a new entry to the `certificates` array:

```json
{
  "id": "GCDM-084",
  "name": "New Participant Name",
  "event": "GitHub Copilot Dev Days | Mumbai",
  "role": "Participant"
}
```

3. Commit and push — the verification page updates automatically.

> ⚠️ Make sure IDs are unique and follow the `GCDM-XXX` format with zero-padded numbers.

---

## 🛠️ Customisation

### Changing the data.json URL

If you rename the repository, update the `DATA_URL` variable inside `index.html`:

```js
var DATA_URL = 'https://raw.githubusercontent.com/SohelPathan0/certificate-verification/main/data.json';
```

### Adding more roles

Simply set the `role` field in `data.json` to anything you need:

```json
{ "id": "GCDM-084", "name": "Speaker Name", "event": "...", "role": "Speaker" }
{ "id": "GCDM-085", "name": "Volunteer Name", "event": "...", "role": "Volunteer" }
```

---

## 📄 License

This project is open for use by community event organisers.  
Feel free to fork and adapt it for your own events.

---

**Powered by Microsoft &amp; GitHub**
