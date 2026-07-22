# KeyAuth Demo Form - Complete Guide

## 🎯 What You Get

This is a **fully functional demo KeyAuth login form** that works immediately without needing a real KeyAuth account. Perfect for:
- Testing UI/UX
- Learning how authentication works
- Development and prototyping
- Building your own custom login system

---

## 🚀 Quick Start (No Setup Needed!)

### 1. **Open the Project**
- Visual Studio → Open `-KeyAuth-CSHARP-Example`
- The project is ready to compile and run

### 2. **Run the Application**
- Press **F5** or click **Run**
- The login form appears immediately

### 3. **Test with Demo Credentials**
Use these demo credentials (shown in the "Demo Creds" button):

```
Username: testuser
Password: testpass123
License Key: TEST-KEY-12345
```

---

## 📋 Form Features

### **Authentication Methods**

| Button | Feature |
|--------|---------|
| **Register** | Create new account with username, password, license key, and email |
| **Login** | Sign in with username and password |
| **License Login** | Authenticate using only a license key |
| **Logout** | End the current session |
| **Demo Creds** | Show test credentials for trying the form |
| **Get KeyAuth** | Instructions to get real KeyAuth account |

---

## 🔧 How to Replace Demo with Real KeyAuth

Once you have a real KeyAuth account, follow these steps:

### **Step 1: Get KeyAuth Account (FREE)**
1. Visit: https://keyauth.cc/
2. Click "Sign Up" → Create account
3. Login: https://keyauth.cc/app/
4. Dashboard opens

### **Step 2: Create Application**
1. Click **Applications** → **Add New**
2. Enter:
   - App Name (e.g., "MyApp")
   - Version (e.g., "1.0")
3. Click **Create**

### **Step 3: Get Your Credentials**
1. Click your app in the dashboard
2. Copy:
   - **App Name** (displayed at top)
   - **Owner ID** (10-character code)
   - **App Secret** (if needed)

### **Step 4: Generate License Keys**
1. In your app dashboard → **Manage Licenses**
2. Click **Generate License**
3. Set:
   - Level (1, 2, 3, etc.)
   - Expiry (days)
   - Amount (how many keys)
4. Click **Generate** → Copy the license key

### **Step 5: Update Your Code**

Open `Form1.cs` and find this section:

```csharp
// ========== CONFIGURATION ==========
private const string APP_NAME = "YourAppName";          // Change this
private const string OWNER_ID = "0000000000";           // 10-char ID from KeyAuth dashboard
private const string APP_VERSION = "1.0";

// Demo credentials for testing (REPLACE WITH YOUR OWN)
private const string DEMO_USERNAME = "testuser";
private const string DEMO_PASSWORD = "testpass123";
private const string DEMO_LICENSE = "TEST-KEY-12345";
```

**Replace with your real credentials:**

```csharp
private const string APP_NAME = "MyApp";                // Your app name
private const string OWNER_ID = "a1b2c3d4e5";          // Your 10-char Owner ID
private const string APP_VERSION = "1.0";

private const string DEMO_USERNAME = "myusername";
private const string DEMO_PASSWORD = "mypassword";
private const string DEMO_LICENSE = "YOUR-LICENSE-KEY"; // Your actual license
```

---

## 🔌 Switching to Real API (Advanced)

To connect to the real KeyAuth API instead of demo mode:

1. **Install NuGet Packages:**
   ```powershell
   Install-Package Newtonsoft.Json -Version 13.0.3
   Install-Package Ed25519 -Version 1.2.3
   ```

2. **Add KeyAuth.cs** (API wrapper from the repository)

3. **Update Form1.cs** to use real API calls:

   ```csharp
   using KeyAuth;
   
   public partial class Form1 : Form
   {
       // Replace demo code with real KeyAuth initialization
       private api KeyAuthApp = new api(
           name: "MyApp",
           ownerid: "a1b2c3d4e5",
           version: "1.0"
       );
       
       private async void Form1_Load(object sender, EventArgs e)
       {
           await KeyAuthApp.init();  // Initialize real KeyAuth connection
       }
       
       private async void btnLogin_Click(object sender, EventArgs e)
       {
           string username = txtUsername.Text.Trim();
           string password = txtPassword.Text.Trim();
           
           await KeyAuthApp.login(username, password);  // Real login
           
           if (KeyAuthApp.response.success)
           {
               // Show success
           }
       }
   }
   ```

---

## 📁 File Structure

```
Project
├── Form1.cs                    # Main form with demo/real logic
├── Form1.Designer.cs           # UI layout
├── KeyAuth.cs                  # Real API wrapper (optional)
├── Program.cs                  # Entry point
└── KEYAUTH_SETUP_GUIDE.md     # This file
```

---

## 🧪 Testing Scenarios

### **Scenario 1: Test Registration**
1. Enter Username: `newuser123`
2. Enter Password: `pass@123`
3. Enter License: `TEST-KEY-99999`
4. Click **Register** → Should succeed

### **Scenario 2: Test Login (Demo)**
1. Enter Username: `testuser`
2. Enter Password: `testpass123`
3. Click **Login** → Should succeed
4. Try wrong password → Should fail

### **Scenario 3: Test License Login**
1. Enter License: `TEST-KEY-12345`
2. Click **License Login** → Should succeed

---

## 🛠️ Customization Ideas

You can customize the form by:

1. **Change Colors** - Edit `Form1.Designer.cs`:
   ```csharp
   this.btnLogin.BackColor = System.Drawing.Color.FromArgb(33, 150, 243);
   ```

2. **Add More Fields** - Add TextBox controls in Designer:
   ```csharp
   private System.Windows.Forms.TextBox txtPhoneNumber;
   ```

3. **Add Validation** - Check password strength:
   ```csharp
   if (password.Length < 8)
   {
       ShowError("Password must be at least 8 characters");
       return;
   }
   ```

4. **Add Forgot Password** - New button:
   ```csharp
   private void btnForgotPassword_Click(object sender, EventArgs e)
   {
       // Open forgot password form
   }
   ```

---

## 📚 KeyAuth Documentation

- **Official Docs:** https://keyauth.readme.io/
- **GitHub:** https://github.com/KeyAuth/KeyAuth-CSHARP-Example
- **Support:** support@keyauth.cc

---

## ❓ FAQ

**Q: Can I use this without KeyAuth account?**  
A: Yes! The demo works standalone with test credentials.

**Q: How do I add real authentication?**  
A: Replace demo code with KeyAuth API calls (see "Switching to Real API" section).

**Q: Is KeyAuth free?**  
A: Yes, basic tier is free! Premium plans available for advanced features.

**Q: Can I distribute this?**  
A: Yes, under the same license as KeyAuth.

**Q: What if I forget my password?**  
A: Click "Get KeyAuth" button → https://keyauth.cc/app/ → Password Reset

---

## 🎓 Next Steps

1. ✅ **Run the demo form** - Test with provided credentials
2. ✅ **Create KeyAuth account** - https://keyauth.cc/
3. ✅ **Generate your first license** - From KeyAuth dashboard
4. ✅ **Replace demo credentials** - Update Form1.cs
5. ✅ **Switch to real API** - Connect KeyAuth.cs to form

---

**You're all set! Start with the demo, then upgrade to real KeyAuth when ready.** 🚀
