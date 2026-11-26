# অ্যাপ টেস্টিং হাব — সেটআপ গাইড

টেস্টাররা একটা লিংকে ঢুকে আপনার সব অ্যাপের ক্লোজ টেস্টিং লিংক পাবে। ফাইল মাত্র দুটো:

- `index.html` — পেজটা (এটা বদলানোর দরকার নেই)
- `apps.json` — আপনার অ্যাপের লিস্ট (শুধু এটাই এডিট করবেন)

## ধাপ ১: Google Group বানানো (একবারই)

1. https://groups.google.com এ গিয়ে **Create group** চাপুন।
2. একটা নাম দিন, যেমন `myapps-testers`।
3. **Who can search for group** → *Anyone on the web*
4. **Who can join group** → *Anyone can join*
5. গ্রুপের লিংক কপি করুন (যেমন `https://groups.google.com/g/myapps-testers`)।

## ধাপ ২: Play Console-এ গ্রুপটা যোগ করা (প্রতিটি অ্যাপে একবার)

Play Console → আপনার অ্যাপ → **Testing → Closed testing** → ট্র্যাক → **Testers** ট্যাব →
**Google Groups** অংশে গ্রুপের ইমেইল দিন (যেমন `myapps-testers@googlegroups.com`) → Save।

এরপর ওই গ্রুপের সবাই এই অ্যাপের টেস্টার হয়ে যাবে।

## ধাপ ৩: পেজটা ফ্রিতে অনলাইনে দেওয়া (GitHub Pages)

1. https://github.com এ একটা অ্যাকাউন্ট খুলুন (না থাকলে)।
2. **New repository** খুলুন → নাম দিন, যেমন `testers` → **Public** রাখুন → Create।
3. **Add file → Upload files** চেপে `index.html` আর `apps.json` আপলোড করুন → Commit।
4. **Settings → Pages** → Source: *Deploy from a branch* → Branch: `main`, ফোল্ডার: `/ (root)` → Save।
5. ১-২ মিনিট পর আপনার লিংক তৈরি হবে: `https://আপনার-ইউজারনেম.github.io/testers/`

এই একটা লিংকই টেস্টারদের দেবেন। এটা কখনো বদলাবে না।

## ধাপ ৪: `apps.json` সেট করা

GitHub-এ `apps.json` খুলে ✏️ (Edit) চাপুন:

```json
{
  "siteTitle": "আমার অ্যাপ টেস্টিং হাব",
  "developerName": "আপনার নাম",
  "googleGroupUrl": "https://groups.google.com/g/myapps-testers",
  "testDays": 14,
  "apps": [
    {
      "name": "আমার ক্যালকুলেটর",
      "packageName": "com.yourname.calculator",
      "description": "সহজ বাংলা ক্যালকুলেটর।",
      "icon": "",
      "status": "testing"
    }
  ]
}
```

## নতুন অ্যাপ ক্লোজ টেস্টিংয়ে গেলে যা করবেন

`apps.json`-এর `apps` লিস্টে একটা ব্লক যোগ করুন (আগের ব্লকের শেষে কমা `,` দিতে ভুলবেন না):

```json
    {
      "name": "নতুন অ্যাপের নাম",
      "packageName": "com.yourname.newapp",
      "description": "ছোট বর্ণনা",
      "icon": "",
      "status": "testing"
    }
```

শুধু **packageName** দিলেই চলবে। "টেস্টার হোন" আর "ইন্সটল করুন" লিংক পেজ নিজেই বানিয়ে নেবে:

- টেস্টার হোন → `https://play.google.com/apps/testing/<packageName>`
- ইন্সটল করুন → `https://play.google.com/store/apps/details?id=<packageName>`

Commit করার ১-২ মিনিট পর পেজে নতুন অ্যাপ দেখা যাবে। কাউকে ইমেইল পাঠাতে হবে না।

### ঐচ্ছিক ফিল্ড

| ফিল্ড | কাজ |
|---|---|
| `icon` | অ্যাপ আইকনের লিংক (`https://` দিয়ে শুরু)। ফাঁকা রাখলে নামের প্রথম অক্ষর দেখাবে। |
| `status` | `"testing"` = ক্লোজ টেস্টিং চলছে, `"live"` = পাবলিশ হয়ে গেছে (শুধু ইন্সটল বাটন দেখাবে) |
| `optInUrl` | Play Console-এর opt-in লিংক আলাদা হলে এখানে দিন |
| `storeUrl` | প্লে স্টোর লিংক আলাদা হলে এখানে দিন |

অ্যাপ প্রোডাকশনে পাবলিশ হয়ে গেলে `"status": "live"` করে দিন।

## টিপস

- JSON-এ ভুল হলে (যেমন কমা বাদ পড়া) পেজ বলবে "লিস্ট লোড করা যায়নি"। তখন https://jsonlint.com এ পেস্ট করে ভুলটা খুঁজে নিন।
- আইকনের লিংক পেতে আইকনটা একই রিপোজিটরিতে আপলোড করুন (যেমন `icons/calculator.png`), তারপর `"icon": "icons/calculator.png"` না দিয়ে পুরো লিংক দিন: `https://আপনার-ইউজারনেম.github.io/testers/icons/calculator.png`

## ডোনেট বাটন

`apps.json`-এর `donate` অংশে `methods` লিস্টে পেমেন্ট মাধ্যম যোগ করলেই পেজে ডোনেট সেকশন আর উপরে "ডোনেট করুন" বাটন দেখাবে। লিস্ট ফাঁকা থাকলে কিছুই দেখাবে না।

মোবাইল ব্যাংকিং নাম্বারের জন্য (টেস্টার "কপি করুন" চেপে নাম্বার কপি করতে পারবে):

```json
{ "name": "bKash (Send Money)", "number": "01XXXXXXXXX", "note": "পার্সোনাল নাম্বার" }
```

লিংকের জন্য (PayPal, Buy Me a Coffee ইত্যাদি):

```json
{ "name": "PayPal", "url": "https://paypal.me/your-name" }
```

`text` আর `title` বদলে নিজের মতো লেখা দিতে পারেন। `quote`-এ কোনো আয়াত বা হাদিস লিখলে সেটা আলাদা করে দেখাবে (ফাঁকা রাখলে দেখাবে না)।
