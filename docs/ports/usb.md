---
title: USB
icon: material/usb
status: done
---

## 1. What Is USB?

**USB** stands for **Universal Serial Bus**.

In simple terms, USB is a **standard way to connect devices** to a computer so they can:

-   🔌 Get **power**
-   📁 Transfer **data**
-   🎮 Communicate (keyboard input, mouse movement, etc.)

USB is everywhere: flash drives, keyboards, mice, phones, webcams, printers, development boards, and more.

## 2. What Problems Does USB Solve?

Before USB, computers had many different ports:

-   **Serial ports**
-   Parallel ports
-   PS/2 (keyboard/mouse)
-   Proprietary connectors

USB unified all of these by providing:

-   **One common connector**
-   **Automatic device detection**
-   **Hot-plugging** (plug/unplug without reboot)
-   **Standard power delivery**

## 3. Basic USB Concepts

### 3.1 Host and Device

USB works in a **master–slave** model:

-   **Host**: Controls the connection
    -   Usually a **PC**, **laptop**, or **smartphone**
-   **Device**: Gets controlled
    -   Keyboard, mouse, USB drive, phone, etc.

📌 Important:

Devices **cannot talk directly to each other** without a host.

### 3.2 USB Cable Has Two Ends

A USB cable is **not symmetric** (except USB-C):

-   **Host side** → connects to computer
-   **Device side** → connects to peripheral

This design enforces the host–device relationship.

## 4. Common USB Connectors

### 4.1 USB Type-A

-   Flat, rectangular
-   Found on PCs, chargers, hubs
-   **Host side**

```
[====]
```

### 4.2 USB Type-B

-   Square with corners cut
-   Used by printers, scanners
-   **Device side**

### 4.3 USB Mini & Micro

-   Older phones, cameras, development boards
-   Micro-USB was very common before USB-C

### 4.4 USB Type-C (Modern Standard)

-   Reversible (no “wrong side”)
-   Can be **host or device**
-   Supports:
    -   Data
    -   Power
    -   Video (DisplayPort / HDMI Alt Mode)

📌 USB-C is a **connector**, not a speed standard.

## 5. USB Versions (Speed Matters)

| USB Version         | Max Speed    | Common Name      |
| ------------------- | ------------ | ---------------- |
| USB 1.1             | 12 Mbps      | Very old         |
| **USB 2.0**         | **480 Mbps** | **Still common** |
| USB 3.0 / 3.2 Gen 1 | 5 Gbps       | “SuperSpeed”     |
| USB 3.2 Gen 2       | 10 Gbps      | Faster           |
| USB4                | 40 Gbps      | High-end         |

📌 A USB-C cable may still run at USB 2.0 speed!

## 6. Power Delivery over USB

USB doesn’t just carry data — it also provides **power**.

### 6.1 Basic Power

-   USB 2.0: up to **2.5 W**
-   USB 3.0: up to **4.5 W**

Enough for:

-   Mouse
-   Keyboard
-   USB flash drive

### 6.2 USB Power Delivery (USB-PD)

Modern USB-C supports **USB-PD**:

-   Up to **240 W**
-   Can power:
    -   Laptops
    -   Monitors
    -   Docking stations

📌 Power is **negotiated** between devices.

## 7. How USB Communication Works (High Level)

When you plug in a USB device:

1.  Host detects a new device
2.  Device identifies itself (class, vendor, product)
3.  Host loads a driver
4.  Data transfer begins

This process is called **enumeration**.

## 8. USB Device Classes (Why Drivers Often “Just Work”)

Many USB devices follow standard **USB classes**:

| Device           | USB Class    |
| ---------------- | ------------ |
| Keyboard / Mouse | HID          |
| Flash Drive      | Mass Storage |
| Webcam           | Video        |
| Audio Interface  | Audio        |

Because of this:

-   No manual driver install needed
-   **Plug and play** works

## 9. USB Hubs

A USB hub:

-   Expands **1 USB port → many ports**
-   Still has **one host**

```
PC ── Hub ── Mouse
        ├─ Keyboard
        ├─ Flash Drive
```

📌 All devices share bandwidth through the hub.

## 10. Common Beginner Confusions

### ❓ USB-C vs USB 3.x

-   USB-C = connector **shape**
-   USB 3.x / USB4 = speed & protocol

You can have:

-   USB-C + USB 2.0 (slow)
-   USB-A + USB 3.0 (fast)

### ❓ Charging Cable vs Data Cable

Some cheap cables:

-   Carry **power only**
-   No data wires inside

Always check cable specs if data transfer fails.

## 11. USB in Daily Life Examples

-   Plugging a flash drive → Mass Storage
-   Phone charging → USB-PD
-   Keyboard input → HID
-   Webcam → USB Video Class

USB is the **hidden infrastructure** behind most peripherals.

## 12. Summary

-   USB = Universal Serial Bus
-   One host controls many devices
-   Carries **data + power**
-   Connector ≠ speed
-   USB-C is modern, flexible, but confusing
-   Plug-and-play works thanks to USB classes

