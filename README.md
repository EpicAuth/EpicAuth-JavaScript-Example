# EpicAuth-JS/TS-Example : Please star 🌟

EpicAuth JavaScript / TypeScript example SDK for https://EpicAuth.cc license key API auth.

_Javascript code is converted from TypeScript using this converter: https://transform.tools/typescript-to-javascript_

**Coded using [bun](https://bun.sh) runtime, it is highly recommended to use bun instead of node or npm, it is faster and way better.**

## **Bugs**

If you are using our example with no significant changes, and you are having problems, please Report Bug here https://EpicAuth.cc/app/?page=forms

However, we do **NOT** provide support for adding EpicAuth to your project. If you can't figure this out you should use Google or YouTube to learn more about the programming language you want to sell a program in.

## Copyright License

EpicAuth is licensed under **Elastic License 2.0**

* You may not provide the software to third parties as a hosted or managed
service, where the service provides users with access to any substantial set of
the features or functionality of the software.

* You may not move, change, disable, or circumvent the license key functionality
in the software, and you may not remove or obscure any functionality in the
software that is protected by the license key.

* You may not alter, remove, or obscure any licensing, copyright, or other notices
of the licensor in the software. Any use of the licensor’s trademarks is subject
to applicable law.

Thank you for your compliance, we work hard on the development of EpicAuth and do not appreciate our copyright being infringed.

## **What is EpicAuth?**

EpicAuth is an Open source authentication system with cloud hosting plans as well. Client SDKs available for [C#](https://github.com/EpicAuth/EpicAuth-CSHARP-Example), [C++](https://github.com/EpicAuth/EpicAuth-CPP-Example), [Python](https://github.com/EpicAuth/EpicAuth-Python-Example), [Java](https://github.com/EpicAuth/EpicAuth-JAVA-api), [JavaScript](https://github.com/EpicAuth/EpicAuth-JavaScript-Example), [VB.NET](https://github.com/EpicAuth/EpicAuth-VB-Example), [PHP](https://github.com/EpicAuth/EpicAuth-PHP-Example), [Rust](https://github.com/EpicAuth/EpicAuth-Rust-Example), [Go](https://github.com/EpicAuth/EpicAuth-Go-Example), [Lua](https://github.com/EpicAuth/EpicAuth-Lua-Examples), [Ruby](https://github.com/EpicAuth/EpicAuth-Ruby-Example), and [Perl](https://github.com/EpicAuth/EpicAuth-Perl-Example). EpicAuth has several unique features such as memory streaming, webhook function where you can send requests to API without leaking the API, discord webhook notifications, ban the user securely through the application at your discretion. Feel free to join https://t.me/EpicAuth if you have questions or suggestions.

## **Customer connection issues?**

This is common amongst all authentication systems. Program obfuscation causes false positives in virus scanners, and with the scale of EpicAuth this is perceived as a malicious domain. So, `EpicAuth.com` and `EpicAuth.cc` have been blocked by many internet providers. For dashboard, reseller panel, customer panel, use `EpicAuth.cc`.

For API, `EpicAuth.cc` will not work because I purposefully blocked it on there so `EpicAuth.cc` doesn't get blocked also. So, you should create your own domain and follow this tutorial video https://www.youtube.com/watch?v=a2SROFJ0eYc. The tutorial video shows you how to create a domain name for 100% free if you don't want to purchase one.

## **`EpicAuthApp` instance definition**

Visit https://EpicAuth.cc/app/ and select your application, then click on the **Javascript** tab.

It'll provide you with the code which you should replace in the `EpicAuth.ts` file.

```typescript
const EpicAuthApp = new EpicAuth({
  name: "", // App name (Manage Applications --> Application name)
  ownerid: "", // Owner ID (Account-Settings --> OwnerID)
  version: "",
});
```

## **Initialize application**

```typescript
await EpicAuthApp.init();
```

## **Display application information**

```typescript
await EpicAuthApp.fetchStats();
console.log(`
App data:
Number of users: ${EpicAuthApp.app_data?.numUsers}
Number of online users: ${EpicAuthApp.app_data?.onlineUsers}
Number of keys: ${EpicAuthApp.app_data?.numKeys}
Application Version: ${EpicAuthApp.app_data?.app_ver}
Customer panel link: ${EpicAuthApp.app_data?.customer_panel}
`);
```

## **Check session validation**

Use this to see if the user is logged in or not.

```typescript
console.log(`Current Session Validation Status: ${await EpicAuthApp.check()}`);
```

## **Check blacklist status**

Check if HWID or IP Address is blacklisted. You can add this if you want, just to make sure nobody can open your program for less than a second if they're blacklisted. Though, if you don't mind a blacklisted user having the program for a few seconds until they try to login and register, and you care about having the quickest program for your users, you shouldn't use this function then. If a blacklisted user tries to login/register, the EpicAuth server will check if they're blacklisted and deny entry if so. So the check blacklist function is just an auxiliary function that's optional.

```typescript
if (await EpicAuthApp.checkblacklist()) {
  console.log("You've been blacklisted from our application.");
  process.exit(1);
}
```

## **Login with username/password**

```typescript
const username = "your_username";
const password = "your_password";
await EpicAuthApp.login(username, password);
```

## **Register with username/password/key**

```typescript
const username = "your_username";
const password = "your_password";
const license = "your_license_key";
await EpicAuthApp.register(username, password, license);
```

## **Upgrade user username/key**

Used so the user can add extra time to their account by claiming a new key.

> [!Warning]
> No password is needed to upgrade the account. So, unlike login, register, and license functions - you should **not** log the user in after a successful upgrade.

```typescript
const username = "your_username";
const license = "your_license_key";
await EpicAuthApp.upgrade(username, license);
```

## **Login with just license key**

Users can use this function if their license key has never been used before, and if it has been used before. So if you plan to just allow users to use keys, you can remove the login and register functions from your code.

```typescript
const license = "your_license_key";
await EpicAuthApp.license(license);
```

## **User Data**

Show information for the current logged-in user.

```typescript
console.log("\nUser data: ");
console.log("Username: " + EpicAuthApp.user_data?.username);
console.log("IP address: " + EpicAuthApp.user_data?.ip);
console.log("Hardware-Id: " + EpicAuthApp.user_data?.hwid);

const subs = EpicAuthApp.user_data?.subscriptions || [];
subs.forEach((sub, index) => {
  const expiry = new Date(sub.expiry * 1000).toISOString();
  console.log(`[${index + 1} / ${subs.length}] | Subscription: ${sub.subscription} - Expiry: ${expiry}`);
});
console.log("Created at: " + new Date(EpicAuthApp.user_data?.createdate * 1000).toISOString());
console.log("Last login at: " + new Date(EpicAuthApp.user_data?.lastlogin * 1000).toISOString());
console.log("Expires at: " + new Date(EpicAuthApp.user_data?.expires * 1000).toISOString());
console.log(`Current Session Validation Status: ${await EpicAuthApp.check()}`);
```

## **Show list of online users**

```typescript
const onlineUsers = await EpicAuthApp.fetchOnline();
let OU = ""; // KEEP THIS EMPTY FOR NOW, THIS WILL BE USED TO CREATE ONLINE USER STRING.
if (!onlineUsers) {
  OU = "No online users";
} else {
  onlineUsers.forEach(user => {
    OU += user.credential + " ";
  });
}

console.log("\n" + OU + "\n");
```

## **Application variables**

A string that is kept on the server-side of EpicAuth. On the dashboard you can choose for each variable to be authenticated (only logged in users can access), or not authenticated (any user can access before login). These are global and static for all users, unlike User Variables which will be discussed below this section.

```typescript
// Get normal variable and print it
const data = await EpicAuthApp.var("varName");
console.log(data);
```

## **User Variables**

User variables are strings kept on the server-side of EpicAuth. They are specific to users. They can be set on Dashboard in the Users tab, via SellerAPI, or via your loader using the code below. `discord` is the user variable name you fetch the user variable by. `test#0001` is the variable data you get when fetching the user variable.

```typescript
// Set up user variable
await EpicAuthApp.setvar("varName", "varValue");
```

And here's how you fetch the user variable:

```typescript
// Get user variable and print it
const data = await EpicAuthApp.getvar("varName");
console.log(data);
```

## **Application Logs**

Can be used to log data. Good for anti-debug alerts and maybe error debugging. If you set Discord webhook in the app settings of the Dashboard, it will send log messages to your Discord webhook rather than store them on site. It's recommended that you set Discord webhook, as logs on site are deleted 1 month after being sent.

You can use the log function before login & after login.

```typescript
// Log message to the server and then to your webhook what is set on app settings
await EpicAuthApp.log("Message");
```

## **Ban the user**

Ban the user and blacklist their HWID and IP Address. Good function to call upon if you use anti-debug and have detected an intrusion attempt.

Function only works after login.

```typescript
await EpicAuthApp.ban();
```

## **Enable Two Factor Authentication (2fa)**

Enable two factor authentication (2fa) on a client account.

```typescript
await EpicAuthApp.enable2fa();
```

## **Disable Two Factor Authentication (2fa)**

Disable two factor authentication (2fa) on a client account.

```typescript
await EpicAuthApp.disable2fa();
```

## **Logout session**

Logout the user's session and close the application. 

This only works if the user is authenticated (logged in).

```typescript
await EpicAuthApp.logout();
```

## **Server-sided webhooks**

Tutorial video https://www.youtube.com/watch?v=ENRaNPPYJbc

> [!NOTE]
> Read documentation for EpicAuth webhooks here https://EpicAuth.readme.io/reference/webhooks-1

Send HTTP requests to URLs securely without leaking the URL in your application. You should definitely use if you want to send requests to SellerAPI from your application, otherwise if you don't use you'll be leaking your seller key to everyone. And then someone can mess up your application.

1st example is how to send request with no POST data. just a GET request to the URL. `7kR0UedlVI` is the webhook ID, `https://EpicAuth.cc/api/seller/?sellerkey=sellerkeyhere&type=black` is what you should put as the webhook endpoint on the dashboard. This is the part you don't want users to see. And then you have `&ip=1.1.1.1&hwid=abc` in your program code which will be added to the webhook endpoint on the EpicAuth server and then the request will be sent.

2nd example includes post data. it is form data. it is an example request to the EpicAuth API. `7kR0UedlVI` is the webhook ID, `https://EpicAuth.cc/api/1.2/` is the webhook endpoint.

3rd examples included post data though it's JSON. It's an example request to Discord webhook `7kR0UedlVI` is the webhook ID, `https://discord.com/api/webhooks/...` is the webhook endpoint.

```typescript
// Example to send normal request with no POST data
const data1 = await EpicAuthApp.webhook("7kR0UedlVI", "&ip=1.1.1.1&hwid=abc");

// Example to send form data
const data2 = await EpicAuthApp.webhook("7kR0UedlVI", "", "type=init&name=test&ownerid=j9Gj0FTemM", "application/x-www-form-urlencoded");

// Example to send JSON
const data3 = await EpicAuthApp.webhook("7kR0UedlVI", "", "{\"content\": \"webhook message here\",\"embeds\": null}", "application/json");
```

## **Download file**

> [!NOTE]
> Read documentation for EpicAuth files here https://docs.EpicAuth.cc/website/dashboard/files

Keep files secure by providing EpicAuth your file download link on the EpicAuth dashboard. Make sure this is a direct download link (as soon as you go to the link, it starts downloading without you clicking anything). The EpicAuth download function provides the bytes, and then you get to decide what to do with those. This example shows how to write it to a file named `text.txt` in the same folder as the program, though you could execute with RunPE or whatever you want.

`385624` is the file ID you get from the dashboard after adding file.

```typescript
// Download Files from the server to your computer using the download function in the api class
const bytes = await EpicAuthApp.file("385624");
const fs = require("fs");
fs.writeFileSync("example.exe", bytes);
```

## **Chat channels**

Allow users to communicate amongst themselves in your program.

Example from the form example on how to fetch the chat messages.

```typescript
// Get chat messages
const messages = await EpicAuthApp.chatGet("CHANNEL");

let Messages = "";
messages.forEach(message => {
  Messages += new Date(message.timestamp * 1000).toISOString() + " - " + message.author + ": " + message.message + "\n";
});

console.log("\n\n" + Messages);
```

Example on how to send chat message.

```typescript
// Send chat message
await EpicAuthApp.chatSend("MESSAGE", "CHANNEL");
```
