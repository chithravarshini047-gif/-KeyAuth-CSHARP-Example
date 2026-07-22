# KeyAuth Windows Forms Integration Setup Guide

## Prerequisites
- Visual Studio 2019 or later
- .NET Framework 4.7.2 or higher
- NuGet Package Manager

## Step 1: Create New Windows Forms Project

```bash
# In Visual Studio:
File > New > Project > Windows Forms App (.NET Framework)
```

## Step 2: Install Required NuGet Packages

### Via Package Manager Console:
```powershell
Install-Package Newtonsoft.Json -Version 13.0.3
Install-Package Ed25519 -Version 1.2.3
```

### Via NuGet Package Manager GUI:
1. Right-click Project > Manage NuGet Packages
2. Search for **Newtonsoft.Json** → Install
3. Search for **Ed25519** → Install

## Step 3: Add Files to Project

Copy the following files to your project:
- `KeyAuth.cs` - API wrapper (main authentication logic)
- `Form1.cs` - Button event handlers
- `Form1.Designer.cs` - UI form design

## Step 4: Configure Your KeyAuth Credentials

1. Go to https://keyauth.cc/app/
2. Log in to your account
3. Copy your:
   - **App Name** (e.g., "MyApp")
   - **Owner ID** (10 characters, e.g., "a1b2c3d4e5")
   - **Version** (e.g., "1.0")

4. Open `Form1.cs` and update the constructor:

```csharp
private api KeyAuthApp = new api(
    name: "YOUR_APP_NAME",        // Replace with your app name
    ownerid: "YOUR_OWNER_ID",     // Replace with your 10-char Owner ID
    version: "1.0"                 // Your app version
);
```

## Step 5: Project File (.csproj) Updates

Add these to your `.csproj` if automatic installation didn't work:

```xml
<ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="13.0.3" />
    <PackageReference Include="Ed25519" Version="1.2.3" />
</ItemGroup>
```

## Step 6: Run and Test

1. Press **F5** or click **Start** in Visual Studio
2. The form will load and initialize KeyAuth
3. Test features:
   - **Register**: Create new account with username, password, and license key
   - **Login**: Sign in with username and password
   - **License Login**: Authenticate using license key only
   - **Logout**: End session

## File Descriptions

| File | Purpose |
|------|---------|
| **KeyAuth.cs** | Core API wrapper handling all KeyAuth communication |
| **Form1.cs** | Event handlers for registration/login/logout buttons |
| **Form1.Designer.cs** | Windows Forms UI layout and controls |

## API Methods Available

### Authentication
- `KeyAuthApp.init()` - Initialize KeyAuth connection
- `KeyAuthApp.register(username, password, licenseKey, email)` - Register new user
- `KeyAuthApp.login(username, password)` - Login with credentials
- `KeyAuthApp.license(licenseKey)` - Login with license key only
- `KeyAuthApp.logout()` - End session

### User Data Access
- `KeyAuthApp.user_data.username` - Get logged-in username
- `KeyAuthApp.user_data.ip` - Get user IP address
- `KeyAuthApp.user_data.hwid` - Get hardware ID
- `KeyAuthApp.user_data.subscriptions[0].subscription` - Get subscription level
- `KeyAuthApp.expirydaysleft()` - Get expiry countdown
- `KeyAuthApp.response.success` - Check if last operation succeeded
- `KeyAuthApp.response.message` - Get response message

## Troubleshooting

### "OwnerID must be 10 characters"
- Verify your Owner ID is exactly 10 characters
- Check https://keyauth.cc/app/ for correct ID

### Build Errors - Missing Packages
```powershell
# Restore packages
Update-Package -Reinstall
```

### SSL Certificate Errors
- Ensure system date/time is correct
- Disable network debugging
- Check internet firewall settings

### "Application not found"
- Verify app name matches KeyAuth dashboard
- Check Owner ID is correct
- Confirm version is set

## Security Notes
- Store credentials securely (don't hardcode in production)
- Use environment variables for sensitive data
- Always validate user input
- Implement rate limiting for brute-force protection

## Support
- KeyAuth Docs: https://keyauth.cc/docs/
- GitHub: https://github.com/KeyAuth/KeyAuth-CSHARP-Example
- Support Email: support@keyauth.cc
