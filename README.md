# Ipfs-Redirect

Create your own IPFS redirect link to help others easily access your IPFS site!

## Introduction

IPFS is a powerful tool for decentralized web hosting, but its adoption has been slow due to accessibility challenges. This project aims to simplify the process of sharing IPFS links by creating an easy-to-use redirect system.

I've been working on this with others in various forums, testing and refining it before making it publicly available. The project includes a small, 26 KB HTML file that acts as a redirect link and a helpful wiki on IPFS usage.

You can access the project via IPFS:
- [Web3 Domain](https://ipfs-redirect.unstoppable/)
- [Web3 Domain Alternative](https://ipfsredirect.unstoppable/)
- [Web3 Version Hosting](https://ipfsredirect-version.unstoppable/)
- [Web2 Domain](https://ipfs.io/ipfs/QmQonrckXZq37ZHDoRGN4xVBkqedvJRgYyzp2aBC5Ujpyp)

The web2 link is the public gateway link to the web2 version which means you won't need Brave browser or extensions. But this is a static link, so you won't be able to see updates. This links to v4 updated on 9/6/24 but I'm not promising to update this link here reliably. Because I'll probably forget. Use the web3 domains for the newest versions.

Youtube video how to use: [Youtube How to Guide](https://www.youtube.com/watch?v=a1QUnEpB83Y&t=4s)

The officially posted versions to the web3 domains. I do try to minify them before publishing. Which usually cuts roughly 30% off the size.

Additionally, when redirecting to web3 domains instead of a CID. The user will get a different screen if they use the link on any browser that's not Brave browser.

**IMPORTANT NOTE***:
Please always reference the Web3 domain created to see what the latest link and CID is. I'll update it over time to any new version. And if you choose to support the project, it'd incredibly appreciated if you keep track of the changes occassionally and pin the newest. Thank you!

## Why This Project?

While IPFS is fast when accessed directly, sharing IPFS sites with others can be challenging. This project provides a solution by offering a redirect link that either sends users directly to the site or guides them through setting up IPFS if needed.

## How the Redirect Works

When you submit a CID or URL, the redirect helper wraps it with the necessary parameters based on your settings. For example, depending on your selections, the redirect might apply origin isolation, use a specific public gateway, or immediately continue to the site without showing IPFS instructions.

At all times, a **"Continue" button** will appear at the bottom-right corner of the screen. If the user clicks it, they’ll skip the IPFS message and proceed with loading the site.

- If the **"Immediate Redirect Continue"** option is enabled, the site will skip the IPFS message entirely and immediately load the spinner followed by the final redirect.

Additionally, there's an option during this loading to **"Click here to load faster!"** which will guide users on how to set up IPFS via a desktop app or browser extension, before redirecting them back to the site.

## Features
## Available Options

### Auto Adapt Link (Disabled in this version)

*Checkbox (Currently Disabled)*

This feature attempts to verify that public gateways are available before redirecting. 

- **If "Requires Origin Isolation" is unchecked**, it will default to:
  ```https://ipfs.io/ipfs/{CID}```

- **If "Requires Origin Isolation" is checked**, it will default to:
  ```https://dweb.link/ipfs/{CID}```

> **Important Note:** This feature has been disabled due to inconsistent results across browsers. In some cases, online gateways weren't properly recognized, causing issues. This will be re-enabled in a future version once reliable performance can be ensured.

---

### Requires Origin Isolation (Subdomain Gateway)

*Checkbox*

Ensures consistent CID retention when navigating across pages within the same IPFS site.

Without this option, navigating via `https://ipfs.io/ipfs/{CID}` might lead to broken links due to URL changes. For example, going from `https://ipfs.io/ipfs/{CID}` to `https://ipfs.io/Your_Page` may lose the CID and cause issues.

Using gateways that support origin isolation, like `dweb.link`, ensures the CID stays consistent.

---

### Web3/2 Domain

*Checkbox*

Use this option to wrap your link using a full Web3 or Web2 domain. It allows URLs that include `http://` or `https://` (or even without them). This is useful for redirecting non-CID links.

---

### Immediate Redirect Continue

*Checkbox*

When enabled, the redirect will skip showing a message about accessing the IPFS site and will immediately start loading.

It applies any set configurations such as Auto Adapt Link, Origin Isolation, and the Magic IPFS Loader, but skips the intermediate message about IPFS, ensuring faster redirection. 

A loading spinner will be displayed while the site loads. 

If this option is not enabled, the user will see a brief message about using IPFS and have the option to manually continue, or follow instructions to improve the load time with the suggested IPFS app or extension.

---

### Redirect Site Has Load Confirmation or MagicIpfsLoader

*Checkbox*

Enabling this option allows the site being redirected to use the `Magic IPFS Loader` or custom confirmation to ensure your site has been fully loaded.

If the destination site includes the script:
```js
window.parent.postMessage('iframeLoaded', '*');
```

### Wiki Capabilities

The main page includes:
- An introduction to IPFS.
- A simple wiki with guides on using and setting up IPFS.
- Best practices for supporting IPFS projects while managing bandwidth.

### Redirect Creator

Creating a redirect link is easy:
1. Navigate to the **Redirect Helper** from the menu.
2. Enter your IPFS CID in the text box.
3. Click **Generate Link**.

This will create a custom redirect URL that integrates your CID.

### How the Redirect Link Works

The generated redirect link is connected to the original CID and customizes the instructions provided to the user. The goal is to be informative without being intrusive.

Key features:
- A **Continue to Site** button that follows the user across pages.
- Automatic wrapping of the CID in an HTTPS gateway if the user hasn't set up IPFS.
- Gateway redundancy to ensure reliability.
- More! I just am too lazy right now to properly document.

## Supporting the Project

Note that the site may load slowly due to limited hosting. Please consider supporting the project by pinning the CID on your IPFS node to improve speed and reliability.
If you appreciate the project, a tip never hurts! Though a pinned CID is just as good ;)
Bitcoin Address: 39oR7Drreu8Dxs2uN7uqWCXet3HkQhd4oS

## Conclusion

This project was a fun and small experiment aimed at making IPFS more accessible. It’s not perfect, but it’s a step toward simplifying decentralized web access. If you find it useful, please consider pinning the CID and spreading the word.
