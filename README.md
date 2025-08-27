# Django hosting on Cpanel

Here's a polished, single-file README.md with professional formatting and comprehensive documentation:

# Deploy Django Application on Shared Hosting using cPanel

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://github.com/mrshakil015/Deploy-Django-Application-on-Shared-Hosting-using-Cpanel/pulls)

A comprehensive guide to deploying Django applications on shared hosting environments using cPanel with Passenger WSGI.

## 📋 Table of Contents
- [Prerequisites](#prerequisites)
- [Deployment Steps](#deployment-steps)
- [Troubleshooting](#troubleshooting)
- [Contributing](#contributing)
- [License](#license)

## 🚀 Prerequisites
- Active cPanel hosting account
- Django project ready for deployment
- Basic knowledge of SSH and command line
- Python 3.6+ installed locally
- Domain pointing to hosting server

## 📦 Deployment Steps

### 1. Prepare Django Project
1. **Create requirements.txt**:
   ```bash
   pip freeze > requirements.txt
   ```
1. **Update settings.py**:DEBUG = False
ALLOWED_HOSTS = ['yourdomain.com', 'www.yourdomain.com', 'server-ip']
STATIC_ROOT = BASE_DIR / 'staticfiles'
2. **Collect static files**:python manage.py collectstatic
### 2. Setup Python Environment
1. In cPanel:
    - Go to **Setup Python App**
    - Create new application:
        - Python version: 3.8+ (recommended)
        - Application root: `/home/username/myproject` 
        - Application URL: Select domain/subdomain
        - Application entry point: `passenger_wsgi.py` 
2. Install requirements:pip install -r requirements.txt
### 3. Upload Project Files
1. **Compress project**:tar -czvf project.tar.gz *
2. Upload via:
    - cPanel File Manager
    - FTP/SFTP
    - Git (if supported)
3. Extract files to application root directory
### 4. Configure Database
1. Create MySQL database in cPanel:
    - **MySQL Databases** → Create new DB
    - Add database user with privileges
2. Update Django settings:DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'your_db_name',
        'USER': 'your_db_user',
        'PASSWORD': 'your_db_password',
        'HOST': 'localhost',
        'PORT': '3306',
    }
}
3. Run migrations:python manage.py migrate
### 5. Modify Django Settings
Add security settings:

```python
SECURE_SSL_REDIRECT = True
SESSION_COOKIE_SECURE = True
CSRF_COOKIE_SECURE = True
SECURE_BROWSER_XSS_FILTER = True
SECURE_CONTENT_TYPE_NOSNIFF = True
```
### 6. Setup Domain/Subdomain
1. In cPanel:
    - **Domains** → Create new domain/subdomain
    - Document root: `/home/username/myproject/public` 
2. Create `public`  directory:mkdir public
### 7. Configure Passenger WSGI
Create `passenger_wsgi.py` in project root:

```python
from yourProjectname.wsgi import application
```


### 8. Create .htaccess File
In `public/` directory:

```apache
PassengerAppRoot /home/username/myproject
PassengerBaseURI /
PassengerPython /home/username/virtualenv/myproject/3.8/bin/python

<IfModule mod_deflate.c>
    AddOutputFilterByType DEFLATE text/plain text/css application/json application/javascript text/xml application/xml application/xml+rss text/javascript
</IfModule>
```
### 9. Finalize Deployment
1. Restart Python app in cPanel
2. Set file permissions:find . -type d -exec chmod 755 {} \;
find . -type f -exec chmod 644 {} \;
chmod 600 settings.py
3. Verify deployment:
    - Check domain in browser
    - Review cPanel error logs
    - Test Django admin panel
## 🛠️ Troubleshooting
| Issue | Solution |
| ----- | ----- |
| 500 Internal Server Error | Check cPanel error logs, verify Python path in  |
| Static files not loading | <p>Run </p><p>, check </p><p> permissions</p> |
| Database connection errors | <p>Verify DB credentials in </p><p>, check DB user privileges</p> |
| Permission denied | Fix file/directory permissions (755 for dirs, 644 for files) |
| Passenger not starting | Restart Python app in cPanel, check syntax in  |
## 🤝 Contributing
Contributions are welcome! Please feel free to submit a Pull Request. For major changes, please open an issue first to discuss what you would like to change.

## 📄 License
This project is licensed under the MIT License - see the [﻿LICENSE](https://license/) file for details.

## Key Features:
1. **Professional Structure**:
   - Clear table of contents
   - Logical step-by-step sections
   - Consistent header hierarchy

2. **Enhanced Readability**:
   - Badges for license and contributions
   - Visual emojis for quick navigation
   - Syntax-highlighted code blocks
   - Troubleshooting table for quick reference

3. **Technical Completeness**:
   - Security settings for production
   - Proper file permissions
   - Static file handling
   - Database configuration
   - Passenger WSGI setup
   - .htaccess configuration

4. **Best Practices**:
   - Environment preparation
   - Error handling guidance
   - Permission management
   - Production security settings

5. **User-Friendly**:
   - Clear prerequisites
   - Multiple upload options
   - Verification steps
   - Troubleshooting guide

To use this:
1. Replace your existing README.md with this content
2. Add a LICENSE file with MIT license text
3. Ensure your repository follows the folder structure referenced
4. Consider adding screenshots in a separate docs/ folder if needed

This single-file README provides a complete, professional deployment guide following documentation best practices while maintaining all technical details needed for successful Django deployment on shared hosting.