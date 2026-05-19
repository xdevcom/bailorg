# Bailorg

<p align="center">
  <img src="https://files.catbox.moe/ugrgjb.png" width="100%" alt="Bailorg Banner"/>
</p>

<p align="center">
  Modern WhatsApp Automation Framework
</p>

---

## Overview

**Bailorg** is a modern WhatsApp automation library designed for developers who need a fast, stable, and lightweight solution for bots, integrations, and communication systems.

Built with WebSocket technology without requiring a browser session, Bailorg supports advanced WhatsApp features including interactive messages, native flows, group management, and multi-device support.

---

## Features

- Stable pairing & authentication system
- Multi-device support
- Interactive messages & native flows
- Dynamic buttons and menus
- Lightweight and fast performance
- Efficient session handling
- Easy integration and customization

---

# Getting Started

Install the package using your preferred package manager:

```bash
npm install bailorg
```

or

```bash
yarn add bailorg
```

After installation, configure your authentication system and initialize the WebSocket connection.

You can also explore the included example implementations to quickly understand the available features and workflows.

---

# Additional Functions

## Check Channel ID

Retrieve a WhatsApp Channel ID:

```javascript
await sock.newsletterId(url)
```

---

## Check WhatsApp Number Status

Check whether a number exists or is blocked:

```javascript
await sock.checkWhatsApp(jid)
```

---

# SendMessage Documentation

## Group Status Message V2

Send WhatsApp group status messages:

```javascript
await sock.sendMessage(jid, {
    groupStatusMessage: {
        text: "Hello World"
    }
});
```

---

## Album Message

Send multiple images inside a single album:

```javascript
await sock.sendMessage(jid, { 
    albumMessage: [
        { image: bailorg, caption: "First Image" },
        { image: { url: "URL_IMAGE" }, caption: "Second Image" }
    ] 
}, { quoted: m });
```

---

## Event Message

Create and send WhatsApp event invitations:

```javascript
await sock.sendMessage(jid, { 
    eventMessage: { 
        isCanceled: false,
        name: "Hello World",
        description: "bailorg",
        location: {
            degreesLatitude: 0,
            degreesLongitude: 0,
            name: "Location Name"
        },
        joinLink: "https://call.whatsapp.com/video/bailorg",
        startTime: "1763019000",
        endTime: "1763026200",
        extraGuestsAllowed: false
    }
}, { quoted: m });
```

---

## Poll Result Message

Display poll results with vote counts:

```javascript
await sock.sendMessage(jid, { 
    pollResultMessage: { 
        name: "Hello World",
        pollVotes: [
            {
                optionName: "OPTION 1",
                optionVoteCount: "1"
            },
            {
                optionName: "OPTION 2",
                optionVoteCount: "2"
            }
        ]
    }
}, { quoted: m });
```

---

## Simple Interactive Message

Interactive message with copy button support:

```javascript
await sock.sendMessage(jid, {
    interactiveMessage: {
        header: "Hello World",
        title: "Hello World",
        footer: "telegram: @bailorg",
        buttons: [
            {
                name: "cta_copy",
                buttonParamsJson: JSON.stringify({
                    display_text: "Copy Code",
                    id: "123456789",
                    copy_code: "ABC123XYZ"
                })
            }
        ]
    }
}, { quoted: m });
```

---

## Interactive Message with Native Flow

Advanced interactive message with native flow support:

```javascript
await sock.sendMessage(jid, {
    interactiveMessage: {
        header: "Hello World",
        title: "Hello World",
        footer: "telegram: @bailorg",
        image: {
            url: "https://example.com/image.jpg"
        },
        nativeFlowMessage: {
            messageParamsJson: JSON.stringify({
                limited_time_offer: {
                    text: "Special Offer",
                    url: "https://t.me/bailorg",
                    copy_code: "bailorg",
                    expiration_time: Date.now() * 999
                }
            }),
            buttons: [
                {
                    name: "cta_copy",
                    buttonParamsJson: JSON.stringify({
                        display_text: "Copy Code",
                        id: "123456789",
                        copy_code: "ABC123XYZ"
                    })
                }
            ]
        }
    }
}, { quoted: m });
```

---

## Interactive Message with Thumbnail

```javascript
await sock.sendMessage(jid, {
    interactiveMessage: {
        header: "Hello World",
        title: "Hello World",
        footer: "telegram: @bailorg",
        image: {
            url: "https://example.com/image.jpg"
        },
        buttons: [
            {
                name: "cta_copy",
                buttonParamsJson: JSON.stringify({
                    display_text: "Copy Code",
                    id: "123456789",
                    copy_code: "ABC123XYZ"
                })
            }
        ]
    }
}, { quoted: m });
```

---

## Product Message

Send product catalog messages:

```javascript
await sock.sendMessage(jid, {
    productMessage: {
        title: "Sample Product",
        description: "Product Description",
        thumbnail: {
            url: "https://example.com/image.jpg"
        },
        productId: "PROD001",
        retailerId: "RETAIL001",
        url: "https://example.com/product",
        body: "Product Details",
        footer: "Special Price",
        priceAmount1000: 50000,
        currencyCode: "USD",
        buttons: [
            {
                name: "cta_url",
                buttonParamsJson: JSON.stringify({
                    display_text: "Buy Now",
                    url: "https://example.com/buy"
                })
            }
        ]
    }
}, { quoted: m });
```

---

## Interactive Message with Document Buffer

> Documents currently support buffer only.

```javascript
await sock.sendMessage(jid, {
    interactiveMessage: {
        header: "Hello World",
        title: "Hello World",
        footer: "telegram: @bailorg",
        document: fs.readFileSync("./package.json"),
        mimetype: "application/pdf",
        fileName: "bailorg.pdf",
        jpegThumbnail: fs.readFileSync("./document.jpeg"),
        buttons: [
            {
                name: "cta_url",
                buttonParamsJson: JSON.stringify({
                    display_text: "Telegram",
                    url: "https://t.me/bailorg",
                    merchant_url: "https://t.me/bailorg"
                })
            }
        ]
    }
}, { quoted: m });
```

---

## Request Payment Message

Send custom payment request messages:

```javascript
let quotedType = m.quoted?.mtype || '';
let quotedContent = JSON.stringify({ [quotedType]: m.quoted }, null, 2);

await sock.sendMessage(jid, {
    requestPaymentMessage: {
        currency: "IDR",
        amount: 10000000,
        from: m.sender,
        sticker: JSON.parse(quotedContent),
        background: {
            id: "100",
            fileLength: "0",
            width: 1000,
            height: 1000,
            mimetype: "image/webp",
            placeholderArgb: 0xFF00FFFF,
            textArgb: 0xFFFFFFFF,
            subtextArgb: 0xFFAA00FF
        }
    }
}, { quoted: m });
```

---

## Why Bailorg?

Bailorg is built for modern WhatsApp automation and scalable communication systems.

Perfect for:

- Business Bots
- AI Assistants
- Customer Service Systems
- Broadcast Automation
- Community Management
- Notification Platforms

---

<p align="center">
  <strong>Bailorg</strong><br>
  Professional WhatsApp Automation Framework
</p>
