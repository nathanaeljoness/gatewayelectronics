Gateway Electronics cPanel Upload Guide

This project is prepared for direct cPanel upload using the `cpanel_ready` folder.

Folder layout:

- `cpanel_ready/public_html/`
  - Upload everything inside this folder into your domain's `public_html/`
- `cpanel_ready/gateway_backend/`
  - Upload everything inside this folder into your Python App root

Steps:

1. Upload `cpanel_ready/public_html/*` to `public_html/`
2. In cPanel, create a Python App with:
   - Application root: `gateway_backend`
   - Application URL: `api`
   - Startup file: `passenger_wsgi.py`
   - Entry point: `application`
3. Upload `cpanel_ready/gateway_backend/*` into that Python App root
4. Create a `.env` file in the Python App root using `.env.example`
5. Install requirements:
   - `pip install -r requirements.txt`
6. Restart the Python App

Test URLs:

- `https://gatewayelectronics.in/api/health`
- `https://gatewayelectronics.in/admin`

If `/api/health` works, the frontend and admin will both use the same backend data.
