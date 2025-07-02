
# 📌 How to Change IP (Set Static IP on Windows)

This guide shows you how to set a **static IP address** for your Ethernet adapter using **Command Prompt (CMD)**.

---

## ✅ 1️⃣ Open Command Prompt as Administrator

- Click **Start** → type `cmd`
- Right-click **Command Prompt** → select **Run as administrator**

---

## ✅ 2️⃣ Find Your Adapter Name

Run:

```bash
netsh interface ipv4 show interfaces
```

Example output:
```
Idx     Met         MTU          State                Name
---  ----------  ----------  ------------  ---------------------------
  1          75        4294967295  connected     Loopback Pseudo-Interface 1
 12          25        1500         connected     Ethernet
 13          45        1500         disconnected  Wi-Fi
```

**Note:** Write down the exact **Name** of your Ethernet adapter. Example: `Ethernet` or `Ethernet 3`.

---

## ✅ 3️⃣ Set the Static IP Address

Replace `Ethernet` with your actual adapter name:

```bash
netsh interface ipv4 set address name="Ethernet" static 192.168.171.2 255.255.255.0 192.168.171.1
```

- `192.168.171.2` → New static IP for your PC.
- `255.255.255.0` → Subnet mask.
- `192.168.171.1` → Gateway (your firewall/router).

---

## ✅ 4️⃣ Set DNS Servers

Add Google DNS (optional):

```bash
netsh interface ipv4 set dns name="Ethernet" static 8.8.8.8
netsh interface ipv4 add dns name="Ethernet" 8.8.4.4 index=2
```

---

## ✅ 5️⃣ Verify

Run:

```bash
ipconfig
```

Check that your **Ethernet adapter** now shows:
```
IPv4 Address. . . . . . . . . : 192.168.171.2
Subnet Mask . . . . . . . . . : 255.255.255.0
Default Gateway . . . . . . . : 192.168.171.1
```

Test connectivity:

```bash
ping 192.168.171.1
```

If you get replies, open your browser and go to:

```
https://192.168.171.1:4444
```

✅ **Done!** You have set a static IP using Command Prompt.
