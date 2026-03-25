# ⚡ Gateway Electronics — Complete Setup Guide

## 📁 Project Structure
```
gateway/
├── frontend/
│   ├── index.html          ← Main website
│   ├── .htaccess           ← Apache routing rules
│   ├── css/styles.css      ← All styles
│   └── js/app.js           ← Frontend logic
├── admin/
│   ├── index.html          ← Admin dashboard
│   ├── css/admin.css       ← Admin styles
│   └── js/admin.js         ← Admin logic
├── backend/
│   ├── app.py              ← Flask API
│   ├── passenger_wsgi.py   ← cPanel entry point
│   ├── requirements.txt    ← Python packages
│   └── .env.example        ← Environment template
└── README.md
```

---

## 🚀 STEP 1 — Set Up MongoDB Atlas (Free)

1. Go to **https://mongodb.com/atlas** → Sign up free
2. Click **"+ Create"** → Choose **M0 Free** → Region: **Mumbai** → Name: `gateway`
3. Create a database user: username + password (save these!)
4. Click **Network Access** → **Add IP Address** → **Allow from Anywhere** (0.0.0.0/0)
5. Click **Connect** → **Drivers** → Copy the connection string:
```
mongodb+srv://USERNAME:PASSWORD@cluster.xxxxx.mongodb.net/gateway_electronics
```
6. Replace `<USERNAME>` and `<PASSWORD>` with your actual credentials

---

## 🚀 STEP 2 — Deploy Frontend to cPanel

1. Log into **GoDaddy cPanel**
2. Open **File Manager**
3. Navigate to `public_html/`
4. Delete any existing `index.html` (default page)
5. Upload these files/folders INTO `public_html/`:
   - `frontend/index.html` → becomes `public_html/index.html`
   - `frontend/.htaccess` → becomes `public_html/.htaccess`
   - `frontend/css/` → becomes `public_html/css/`
   - `frontend/js/` → becomes `public_html/js/`
6. Create folder `public_html/admin/`
7. Upload these into `public_html/admin/`:
   - `admin/index.html`
   - `admin/css/`
   - `admin/js/`

---

## 🚀 STEP 3 — Set Up Python Backend in cPanel

1. In cPanel, find **"Setup Python App"**
2. Click **"Create Application"**:
   - **Python version**: Choose highest available (3.x)
   - **Application root**: `gateway_backend` (new folder)
   - **Application URL**: `api`  ← This makes it accessible at gatewayelectronics.in/api
   - **Application startup file**: `passenger_wsgi.py`
   - **Application Entry point**: `application`
3. Click **"Create"**

4. You'll see a terminal command like:
```bash
source /path/to/virtualenv/bin/activate && cd /path/to/app
```
Copy and run it in the **cPanel terminal**

5. Install packages:
```bash
pip install flask flask-cors pymongo python-dotenv
```

6. Upload backend files to the `gateway_backend/` folder in File Manager:
   - `backend/app.py`
   - `backend/passenger_wsgi.py`
   - `backend/requirements.txt`

7. Create a `.env` file in `gateway_backend/`:
```
MONGO_URI=mongodb+srv://USERNAME:PASSWORD@cluster.xxxxx.mongodb.net/gateway_electronics
```

8. Back in Python App → click **"Restart"**

---

## 🚀 STEP 4 — Connect Frontend to Backend

Open `public_html/js/app.js` and update the API constant:
```javascript
// Change this line at the top:
const API = '/api';
// It should already be '/api' — no change needed if Python App is set to URL: api
```

Open `public_html/admin/js/admin.js` and update:
```javascript
const API = '/api';  // Already set correctly
```

---

## 🚀 STEP 5 — Test Everything

1. Visit **https://gatewayelectronics.in** → Website loads ✅
2. Visit **https://gatewayelectronics.in/api/health** → Shows `{"status":"ok","db":"connected"}` ✅
3. Visit **https://gatewayelectronics.in/api/laptops** → Shows laptop listings ✅
4. Visit **https://gatewayelectronics.in/admin** → Admin login page ✅
   - Username: `gatewayelectronics`
   - Password: `lexi.6002`

---

## 🔑 Admin Panel Features

| Feature | Description |
|---------|-------------|
| **Overview** | Stats: total laptops, orders, sell requests, messages |
| **Manage Laptops** | Add, edit, delete laptop listings |
| **Orders** | View all customer orders with items and total |
| **Sell Requests** | View all laptop sell/buyback requests |
| **Messages** | View all contact form submissions |

---

## 📱 Website Features

- Black + Gold + White luxury theme
- Original price shown in **RED** (strikethrough)
- Selling price shown in **WHITE**
- Filter laptops by brand (Apple, Dell, Lenovo, HP, Asus, Surface)
- Cart → Order form → Saved to MongoDB + WhatsApp notification
- Sell your laptop form → Saved to MongoDB
- Repair services section
- About Us with animated stats
- Contact form
- Floating WhatsApp button (+91 9994211512)
- Fully mobile responsive
- Subtle parallax animations

---

## ⚙️ Running Locally (for testing)

```bash
# Terminal 1 — Backend
cd backend
pip install -r requirements.txt
python app.py
# API runs at http://localhost:5000

# Terminal 2 — Frontend
# Just open frontend/index.html in browser
# OR use VS Code Live Server
```

---

## 📞 Support
WhatsApp: +91 9994211512
Email: mkphdmkphd@gmail.com
