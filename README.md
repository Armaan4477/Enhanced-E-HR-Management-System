# Enhanced E-HR Management System

A comprehensive HR management system built using Python with Tkinter for the GUI and Firebase Realtime Database for data storage.

## Screenshots
![E-HR System Login Screen](screenshots/login.png)
    This is the login screen where users can enter their credentials based on their role.

![E-HR System Admin Dashboard](screenshots/admin.png)
    This is the dashboard view showing the main Admin interface for managing functions.

![E-HR System HR Dashboard](screenshots/hr.png)
    This is the dashboard view showing the main HR interface for managing functions.

![E-HR System Manager Dashboard](screenshots/manager.png)
    This is the dashboard view showing the main Manager interface for managing functions.

![E-HR System Employee Dashboard](screenshots/employee.png)
    This is the dashboard view showing the main Employee interface for managing functions.

## Features

- Multi-role access system (Admin, HR, Manager, Employee)
- Comprehensive user management
- Performance review system
- Vacation and sick leave management
- Resignation request processing
- Promotion and bonus request systems
- Employee surveys and feedback collection
- Complaint management
- Secure authentication
- Persistent data storage using Firebase

## Prerequisites

- Python 3.12 or higher
- Firebase account
- Internet connection for database access

## Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/YourUsername/Enhanced-E-HR-Management-System.git
   cd Enhanced-E-HR-Management-System
   ```

2. Install the required dependencies:
   ```bash
   pip install -r requirements.txt
   ```

## Firebase Setup

### 1. Create a Firebase Project

1. Go to the [Firebase Console](https://console.firebase.google.com/)
2. Click "Add project" and follow the setup wizard
3. Give your project a name (e.g., "E-HR Management System")
4. Follow the prompts to complete the setup

### 2. Set up Realtime Database

1. In the Firebase Console, select your project
2. Click on "Realtime Database" in the left sidebar
3. Click "Create Database"
4. Start in test mode for development (You'll set up proper security rules later)
5. Choose a database location closest to your users

### 3. Import Database Structure

1. In the Realtime Database section, click the overflow menu (three dots) and select "Import JSON"
2. Upload the provided `ehr-management-system-export.json` file
3. This will populate your database with the required structure and some initial data

### 4. Set Database Rules

1. In the Realtime Database section, click the "Rules" tab
2. Replace the existing rules with the contents of the provided `rules.txt` file
3. Click "Publish"

### 5. Generate Firebase Credentials

1. In the Firebase Console, go to Project Settings (gear icon)
2. Click on the "Service Accounts" tab
3. Click "Generate new private key"
4. Save the downloaded JSON file as `credentials.json` in your project directory
5. Open the `credentials.json` file and add the `databaseURL` field manually:

```json
{
  "type": "service_account",
  "project_id": "your-project-id",
  "private_key_id": "your-private-key-id",
  "private_key": "-----BEGIN PRIVATE KEY-----\nYour Private Key\n-----END PRIVATE KEY-----\n",
  "client_email": "firebase-adminsdk-xxxxx@your-project-id.iam.gserviceaccount.com",
  "client_id": "your-client-id",
  "auth_uri": "https://accounts.google.com/o/oauth2/auth",
  "token_uri": "https://oauth2.googleapis.com/token",
  "auth_provider_x509_cert_url": "https://www.googleapis.com/oauth2/v1/certs",
  "client_x509_cert_url": "https://www.googleapis.com/robot/v1/metadata/x509/firebase-adminsdk-xxxxx%40your-project-id.iam.gserviceaccount.com",
  "universe_domain": "googleapis.com",
  "databaseURL": "https://your-project-id-default-rtdb.firebaseio.com"
}
```

> **Important**: Replace `https://your-project-id-default-rtdb.firebaseio.com` with your actual Firebase Realtime Database URL, which you can find in the Realtime Database section of the Firebase Console.

### 6. Create encrypted_credentials.txt
1. Run the `encrypt_credentials.py` script to create an encrypted version of your credentials:
   ```bash
   python encrypt_credentials.py
   ```
2. This will create a file named `encrypted_credentials.txt` in the same directory as `main.py`.
3. Ensure that `encrypted_credentials.txt` is in the same directory as `main.py` for the system to work.
4. The script will also verify that the encryption works by attempting to decrypt the credentials.
5. If successful, you will see a message indicating that the credentials were successfully decrypted.

## Running the Application

Execute the main Python script:

```bash
python main.py
```

## User Roles and Functionality

### Admin
- Create/remove user logins
- Approve resignations
- Access all system modules
- Login as other roles

### HR Manager
- Manage employee records
- Handle salary management
- Process leave requests
- Review performance evaluations
- Handle complaints

### Manager
- Approve performance reviews
- Approve leave requests
- Request employee promotions
- Approve resignations
- Request bonuses

### Employee
- Apply for leave
- Submit resignation requests
- Complete surveys
- Submit complaints
- Submit performance reviews

## Keyboard Shortcuts

- `Escape` to exit current window
- `Enter` to submit forms or login

## Project Structure

```
Enhanced-E-HR-Management-System/
├── main.py              # Main application launcher
├── Admin.py             # Admin functionality
├── HR.py                # HR functionality
├── Manager.py           # Manager functionality
├── Employee.py          # Employee functionality
├── requirements.txt     # Python dependencies
├── credentials.json     # Firebase credentials (you must create this)
├── encrypted_credentials.txt # Encrypted credentials
├── encrypt_credentials.py # Script to encrypt credentials
├── README.md            # This file
└── images/              # Application images
│    ├── HR_background.png
│    ├── profile.png
│    └── logout.png
├── database_backup/
    ├── ehr-management-system-export.json
    └── rules.txt
```

## Troubleshooting

- If you see a Firebase initialization error, check your credentials.json file and ensure the databaseURL is correct
- Make sure your Firebase Realtime Database has been initialized and is in the correct region
- Verify that all the required images are in the images/ directory

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Building the app with PyInstaller

When ready to compile the app:

```bash
pip install pyinstaller
```
Then run the following command in the terminal:

```bash
pyinstaller --windowed \
          --name="E-HR Mgnt System" \
          --add-data="images:images" \
          --add-data="encrypted_credentials.txt:." \
          --add-data "Admin.py:." \
          --add-data "Employee.py:." \
          --add-data "Manager.py:." \
          --add-data "HR.py:." \
          main.py
```

This will:
- Bundle the encrypted credentials file with your app
- Keep your Firebase credentials secure
- Maintain the full functionality of your app
