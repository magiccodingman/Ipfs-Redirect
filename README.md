# Ipfs-Redirect

Create your own IPFS redirect link to help others easily access your IPFS site!

## Introduction

IPFS is a powerful tool for decentralized web hosting, but its adoption has been slow due to accessibility challenges. This project aims to simplify the process of sharing IPFS links by creating an easy-to-use redirect system.

### How the Redirect Link Works

The generated redirect link is connected to the original CID and customizes the instructions provided to the user. The goal is to be informative without being intrusive.

Key features:
- A **Continue to Site** button that follows the user across pages.
- Automatic wrapping of the CID in an HTTPS gateway if the user hasn't set up IPFS.
- Gateway redundancy to ensure reliability.
- More! I just am too lazy right now to properly document.

### Links, Guides, and Notes

I've been working on this with others in various forums, testing and refining it before making it publicly available. The project includes a small, 26 KB HTML file that acts as a redirect link and a helpful wiki on IPFS usage.

You can access the project via IPFS:
- [Web3 Domain (ipfs-redirect.unstoppable)]([https://ipfs-redirect.unstoppable/](https://ipfs.io/ipfs/bafybeigegkxhaz7txa7lg5zaur3svwghdwkrcqvfnjpdg6ji5ldmuguoz4?redirectURL=ipfsredirect.unstoppable&autoadapt=0&requiresorigin=0&web3domain=1&immediatecontinue=1&magiclibraryconfirmation=0&resolveweb3domain=1))

Youtube video how to use: [Youtube How to Guide](https://www.youtube.com/watch?v=a1QUnEpB83Y)
Youtube video how to use (Web3 Resolving Feature Update): [Youtube How to Guide (Web3 Resolving)]([https://www.youtube.com/watch?v=a1QUnEpB83Y](https://www.youtube.com/watch?v=U_HAfjXbNNM))

Also you can go to my site at [magic coding man ipfs redirect link](https://magiccodingman.com/Ipfs-Redirect) to see an updated guide and article.

**IMPORTANT NOTE***:
Please always reference the Web3 domain created to see what the latest link and CID is. I'll update it over time to any new version. And if you choose to support the project, it'd incredibly appreciated if you keep track of the changes occassionally and pin the newest. Thank you!

## Why This Project?

While IPFS is fast when accessed directly, sharing IPFS sites with others can be challenging. This project provides a solution by offering a redirect link that either sends users directly to the site or guides them through setting up IPFS if needed.

## How the Redirect Works

When you submit a CID or URL, the redirect helper wraps it with the necessary parameters based on your settings. For example, depending on your selections, the redirect might apply origin isolation, use a specific public gateway, or immediately continue to the site without showing IPFS instructions.

At all times, a **"Continue" button** will appear at the bottom-right corner of the screen. If the user clicks it, they’ll skip the IPFS message and proceed with loading the site.

- If the **"Immediate Redirect Continue"** option is enabled, the site will skip the IPFS message entirely and immediately load the spinner followed by the final redirect.

Additionally, there's an option during this loading to **"Click here to load faster!"** which will guide users on how to set up IPFS via a desktop app or browser extension, before redirecting them back to the site.


## Available Options

### Auto Adapt Link (Disabled in v4)

*Checkbox*

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

This feature ensures that the redirect process doesn't complete until the target site has fully loaded, preventing partial or failed loads, especially when using public IPFS gateways.

#### How It Works

When you enable this option, the Redirect Helper will look for a specific confirmation signal from the redirected-to site to verify that the site has successfully loaded. This confirmation is triggered by a line of JavaScript code that you need to add to the site being redirected to:

If the destination site includes the script:
```js
window.parent.postMessage('iframeLoaded', '*');
```

The redirect helper loads your site within an iframe and monitors for this confirmation message. If the message is received, it signals that the site has fully loaded, and the user is then redirected to the site seamlessly. If the message isn't received within the 5-minute window, the iframe is removed, and the site reloads the iframe. This process is repeated every 5 minutes, forcing the IPFS public gateway to continue searching for your site until it's successfully found and loaded.

#### Why It's Important

- **Preventing Timeout Errors:** Without this feature, if the public IPFS gateway fails to locate your site within the 5-minute timeout period, the user will encounter a `500 Timeout Error`, which can be a frustrating dead-end experience. By reloading the iframe and continuing to search for the site, the redirect helper increases the likelihood that your site will eventually load, rather than timing out.
  
- **Ensuring Full Site Load:** In some cases, the initial load might bring up the `index.html` file, but crucial resources like CSS, JavaScript frameworks, or other dependencies might not have fully loaded. This can result in a broken or incomplete experience for users. By adding the confirmation code only after these critical files are loaded, you ensure that the redirect happens only when your site is fully functional. You can choose to trigger the confirmation message either as soon as `index.html` loads, or after specific critical resources (like your framework, bootstrap, or JavaScript) have successfully loaded.

#### Integration with Magic IPFS Loader

Currently, you need to manually add the confirmation code to the redirected site. However, in the near future, the **Magic IPFS Loader** will handle this automatically. Once integrated, you won't need to add any custom code—**Magic IPFS Loader** will automatically confirm that all critical resources (not just the `index.html`) have been successfully fetched before completing the redirect.

This ensures that users don’t just see the site, but they interact with a fully loaded and functioning version of your IPFS site. The loader will retry fetching critical files until they are successfully retrieved, preventing incomplete site loads.

> **Note:** Until the Magic IPFS Loader is fully released and integrated, it’s recommended to add the confirmation code manually to ensure optimal loading. Without this, the redirect helper won't know if your site has fully loaded and may cause premature redirection, leading to incomplete or broken user experiences.

---

By using the load confirmation feature, you ensure your users are taken to a fully functioning version of your site, without running into public gateway timeouts or missing critical files. This is especially useful in environments where public gateways might be slow or unreliable.

### Wiki Capabilities

The main page includes:
- An introduction to IPFS.
- A simple wiki with guides on using and setting up IPFS.
- Best practices for supporting IPFS projects while managing bandwidth.

### Redirect Helper

Creating a redirect link is easy:
1. Navigate to the **Redirect Helper** from the menu.
2. Enter your IPFS CID in the text box.
3. Click **Generate Link**.

This will create a custom redirect URL that integrates your CID.

## Supporting the Project

Note that the site may load slowly due to limited hosting. Please consider supporting the project by pinning the CID on your IPFS node to improve speed and reliability.
If you appreciate the project, a tip never hurts! Though a pinned CID is just as good ;)
Bitcoin Address: 39oR7Drreu8Dxs2uN7uqWCXet3HkQhd4oS

## Conclusion

This project was a fun and small experiment aimed at making IPFS more accessible. It’s not perfect, but it’s a step toward simplifying decentralized web access. If you find it useful, please consider pinning the CID and spreading the word.
