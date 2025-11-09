# How to Change a Public Network to Private in Windows 11 Using PowerShell

## 📘 Overview
By default, when Windows 11 connects to a **new network**, it sets the **network type to Public**.  
This enhances security by hiding your device from other computers on the same network.  

However, for **trusted networks** (like home or office LANs), you may need to switch from **Public** to **Private** to enable:
- 🖨️ Printer sharing  
- 📁 File sharing  
- 🎮 Local multiplayer gaming  
- 🧩 Network discovery and management  

This guide explains how to change your network type using **PowerShell** — a quick and reliable method for administrators.

---

## 🧰 Prerequisites

| Requirement | Description |
|--------------|-------------|
| 🪟 Operating System | Windows 10 or Windows 11 |
| ⚙️ Permissions | Run PowerShell as **Administrator** |
| 🌐 Network | You must already be **connected** to the network you want to modify |

---

## ⚙️ Step 1 — Open PowerShell as Administrator

1. Press **`Win + X`** and choose **Windows Terminal (Admin)** or **PowerShell (Admin)**  
2. Confirm the UAC prompt with **Yes**

💡 *Administrative privileges are required to change network categories.*

---

## 🔍 Step 2 — View Current Network Profile

Run the following command to list all active network profiles:

```powershell
Get-NetConnectionProfile
````

This command displays:

| Field               | Description                                                                    |
| ------------------- | ------------------------------------------------------------------------------ |
| **Name**            | The network name (SSID or Ethernet identifier)                                 |
| **InterfaceAlias**  | The adapter name (e.g., `Wi-Fi` or `Ethernet`)                                 |
| **NetworkCategory** | Indicates whether the network is `Public`, `Private`, or `DomainAuthenticated` |

🧩 **Example Output:**

```
Name             : MyHomeWiFi
InterfaceAlias   : Wi-Fi
NetworkCategory  : Public
```

---

## 🛠️ Step 3 — Change Network from Public to Private

Now that you know your network’s name, run the following command — replacing `NetworkName` with your own:

```powershell
Set-NetConnectionProfile -Name "NetworkName" -NetworkCategory Private
```

✅ This command changes the specified network’s category to **Private**.

🧩 **Example:**

```powershell
Set-NetConnectionProfile -Name "MyHomeWiFi" -NetworkCategory Private
```

---

## 🔎 Step 4 — Verify the Change

Run the same command from **Step 2** again:

```powershell
Get-NetConnectionProfile
```

If successful, the **NetworkCategory** should now show:

```
NetworkCategory : Private
```

---

## ⚠️ Important Security Note

> 🔒 **Never set a public Wi-Fi network (e.g., airport, coffee shop, or hotel) to Private.**

Doing so allows your device to become discoverable to others on that network, which poses a security risk.
Only switch to **Private** on **trusted** networks (like home or office).

---

## 🧠 Troubleshooting Tips

| Issue                                     | Solution                                                                     |
| ----------------------------------------- | ---------------------------------------------------------------------------- |
| `Access Denied` error                     | Make sure PowerShell is run as **Administrator**                             |
| No output from `Get-NetConnectionProfile` | Ensure the network adapter is **connected and active**                       |
| Name mismatch                             | Verify you’re using the **exact network name** as shown in the first command |

---

## 🚀 Bonus — Change All Networks to Private (Optional)

To set **all active networks** to Private in one go, use:

```powershell
Get-NetConnectionProfile | Set-NetConnectionProfile -NetworkCategory Private
```

⚠️ Use this carefully — it will modify every connected network profile on the system.

---

## ✅ Summary

By following these steps, you can easily and safely switch your network type from **Public** to **Private** using PowerShell.

| Step | Command                                                            | Description                  |
| ---- | ------------------------------------------------------------------ | ---------------------------- |
| 1️⃣  | `Get-NetConnectionProfile`                                         | View current network profile |
| 2️⃣  | `Set-NetConnectionProfile -Name "<Name>" -NetworkCategory Private` | Change network to private    |
| 3️⃣  | `Get-NetConnectionProfile`                                         | Verify change                |

---

## 🧑‍💻 Document Metadata

| Field            | Detail                                             |
| ---------------- | -------------------------------------------------- |
| **Author**       | Xitiz Basnet                                       |
| **Category**     | Networking / PowerShell                            |
| **Tags**         | Network Profiles, PowerShell, Security, Windows 11 |

---

> 🏁 **End of Document**
> *Use this PowerShell method only on trusted networks such as home or office connections.*

---

 
