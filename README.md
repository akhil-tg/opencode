<div align="center">

# ⚡ OpenCode Free Usage Limit Fix

### Troubleshooting `Free usage limit reached` on Windows

![Windows](https://img.shields.io/badge/OS-Windows_11-blue?logo=windows)
![OpenCode](https://img.shields.io/badge/OpenCode-v2.3.0-purple)
![Status](https://img.shields.io/badge/Status-Success-brightgreen)

</div>

---

## 📌 Table of Contents

- [The Problem](#-the-problem)
- [System Information](#-system-information)
- [Initial Investigation](#-initial-investigation)
- [Checking Public IP](#-checking-public-ip)
- [Changing Network Connection](#-changing-network-connection)
- [VPN Testing](#-vpn-testing)
- [Final Test Results](#-final-test-results)
- [Daily Workflow](#-daily-workflow)
- [Useful Commands](#-useful-commands)
- [Security Notes](#-security-notes)
- [Conclusion](#-conclusion)

---

## 🚨 The Problem

While using OpenCode CLI, the following error appeared:

```text
You've used today's free messages.
They reset at 6:07 AM.
```

Even after trying different OpenCode accounts and API keys, the error continued.

### Initial troubleshooting

- Switched between different OpenCode accounts.
- Generated different API keys.
- Restarted OpenCode.
- Tried different free models.
- Changed network connections.
- Connected through a VPN.

Changing accounts and API keys alone did not solve the issue.

---

## 💻 System Information

| Component | Details |
|---|---|
| Operating System | Windows 11 |
| Terminal | CMD / PowerShell |
| OpenCode Version | v2.3.0 |
| Authentication | OpenCode Console |
| Connection | Wi-Fi / VPN |
| Issue | Free usage limit reached |

### Check OpenCode Version

```powershell
opencode --version
```

### Check Authentication

```powershell
opencode auth list
```

### List Available Models

```powershell
opencode models
```

---

## 🔍 Initial Investigation

Tested different free models.

### Test 1: Big Pickle

```powershell
opencode run --model opencode/big-pickle "Hello"
```

Result:

```text
Error: Free usage limit reached.
```

### Test 2: GLM 5.3 Flash Free

```powershell
opencode run --model opencode/glm-5.3-flash-free "Hello"
```

Result:

```text
Error: Free usage limit reached.
```

Both models were blocked on the original network connection.

---

## 🌐 Checking Public IP

To investigate whether the network connection was involved, I checked my public IP address.

### Command

```cmd
curl.exe https://api.ipify.org
```

The command returned the public IP assigned by the internet connection.

**Note:** Actual IP addresses are intentionally excluded from this documentation for privacy.

---

## 🔄 Changing Network Connection

Several methods can change your network connection or IP address.

### Method 1: Renew Local IP

Open CMD as Administrator:

```cmd
ipconfig /release
ipconfig /renew
ipconfig /flushdns
```

**Note:** These commands renew local network configuration. They do not guarantee a public IP change.

### Method 2: Restart Router

1. Turn off the router.
2. Wait 5–10 minutes.
3. Turn it back on.
4. Check your public IP.

Whether the public IP changes depends on your ISP.

### Method 3: Mobile Hotspot

1. Disconnect from Wi-Fi.
2. Enable mobile hotspot on your phone.
3. Connect your computer.
4. Check your public IP.

This method was considered but not confirmed in the final tests.

---

## 🔐 VPN Testing

Next, I connected to a VPN and checked the public IP again.

### Command

```cmd
curl.exe https://api.ipify.org
```

The command returned a different public IP after connecting to the VPN.

**Result:** VPN connection successfully changed the public IP.

Actual IP addresses are intentionally not disclosed.

---

## ✅ VPN Testing – Successful Result

With the VPN connected, I tested the same OpenCode models again.

### Test 1: Big Pickle

```cmd
opencode run --model opencode/big-pickle "Reply only OK"
```

Output:

```text
> build · big-pickle
OK
```

**Status: SUCCESS ✅**

### Test 2: GLM 5.3 Flash Free

```cmd
opencode run --model opencode/glm-5.3-flash-free "Reply only OK"
```

Output:

```text
> build · glm-5.3-flash-free
OK
```

**Status: SUCCESS ✅**

Both models worked successfully without changing the existing OpenCode authentication.

---

## 📊 Final Test Results

| Test | Normal Network | VPN |
|---|---|---|
| Big Pickle | ❌ Failed | ✅ Success |
| GLM 5.3 Flash Free | ❌ Failed | ✅ Success |
| Public IP | Original IP | Different IP |
| OpenCode Authentication | Existing account | Same account |

### What We Learned

- Changing accounts did not solve the problem.
- Generating additional API keys did not solve the problem.
- Connecting through a VPN coincided with successful model requests.
- Both tested free models worked through the VPN.
- Existing OpenCode authentication was sufficient.

**Important:** This strongly suggests that the original network connection or its associated IP reputation was involved. However, these tests do not conclusively prove that OpenCode uses IP-based quota enforcement.

---

## ⚡ Daily Workflow

Once the VPN is connected, follow these steps.

### Step 1: Connect VPN

Connect to your preferred VPN server.

### Step 2: Verify Public IP

```cmd
curl.exe https://api.ipify.org
```

### Step 3: Navigate to Your Project

```cmd
cd C:\path\to\your\project
```

### Step 4: Start OpenCode

```cmd
opencode
```

### Step 5: Start Coding

Continue using your preferred OpenCode models.

---

## 🛠️ Useful Commands

| Purpose | Command |
|---|---|
| OpenCode version | `opencode --version` |
| Authentication | `opencode auth list` |
| Available models | `opencode models` |
| Check public IP | `curl.exe https://api.ipify.org` |
| Renew local IP | `ipconfig /renew` |
| Release local IP | `ipconfig /release` |
| Flush DNS | `ipconfig /flushdns` |

### Test Big Pickle

```powershell
opencode run --model opencode/big-pickle "Reply only OK"
```

### Test GLM Free

```powershell
opencode run --model opencode/glm-5.3-flash-free "Reply only OK"
```

---

## 🔒 Security Notes

- Never publish your OpenCode Console API key.
- Never upload API keys to GitHub.
- Revoke exposed API keys immediately.
- Use secure authentication storage.
- Do not commit personal IP addresses or authentication credentials to public repositories.

---

## 🎯 Conclusion

The original problem appeared to be related to the network connection rather than the local OpenCode installation.

Connecting through a VPN changed the public IP address, after which both Big Pickle and GLM 5.3 Flash Free successfully generated responses.

The same account and authentication worked without generating additional API keys.

### Final Working Configuration

```text
Windows 11
    |
    v
OpenCode CLI v2.3.0
    |
    v
OpenCode Console Authentication
    |
    v
VPN Connection
    |
    v
OpenCode Free Models
    |
    v
SUCCESS
```

---

<div align="center">

### ⭐ Happy Coding! 🚀

</div>
