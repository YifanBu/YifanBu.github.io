---
title: "Ecommerce Tracking with Google Tag Manager"
date: 2020-05-11
tags: [Google Tag Manager, Ecommerce]
header:
image:
excerpt: "Digital Analytics"
toc: true
toc_label: "Table of Contents"
toc_sticky: true
toc_icon: "cog"
---

# What is GA Ecommerce Tracking?

By doing some additional configuration, you can start tracking sales with Google Analytics. All thanks to Ecommerce tracking features. By implementing them, you will be able to measure the number of transactions, revenue that your website generates, etc.

Once a user completes a purchase (and is redirected to the Order Confirmation page) this moment can be captured by Google Analytics. By sending transaction data to GA (like Order Total or Purchased products) you’ll unlock new reporting possibilities and will start seeing how your marketing efforts are actually impacting online sales.

## Two main types

1. **Standard Ecommerce**: allow you to analyze purchase activity on your site or app. You can see product and transaction information, average order value, ecommerce conversion rate, time to purchase, and other data.

2. **Enhanced Ecommerce**: shows when customers added items to their shopping carts, when they started the checkout process, and when they completed a purchase. You can also use enhanced ecommerce to identify segments of customers who fall out of the shopping funnel. 

## Which Ecommerce option to choose

If you want to see only sales data and how well each product performs, which traffic sources generate sales, then choose Standard Ecommerce functionality.

If you want to see not only purchases but visitor’s journey as well (data related to Add to cart activity, Checkout steps, etc.), then Enhanced Ecommerce should be your option.

However, it is much more difficult to implement Enhanced Ecommerce functionality, additionally, it requires much more developer’s time to get things going. Therefore, you’d need to weigh your options. With EE, you’ll get much more insights, but it’s much more expensive to properly implement.

# Implementation plan

Here’s the plan that you’ll need to follow:

1. First, you’ll need to enable Ecommerce Reports in Google Analytics
2. Then you’ll need to ask a developer to push a transaction data to the Data Layer (or get a plugin for that purpose, if possible)
3. Send the Ecommerce transaction data to Google Analytics (via Google Tag Manager)
4. Test if everything is working properly

## Enable Ecommerce Reports in GA

Admin -> View -> Ecommerce Settings -> Ecommerce set-up -> Enable Ecommerce

## dataLayer setup

In order to make GA Ecommerce tracking with Google Tag Manager work, first, we need to get the transaction data pushed to the dataLayer after a purchase is successfully completed. Then, we’ll instruct GTM to read that data and transfer it to Google Analytics.

### Ecommerce code to push

The whole process is like this:

- A developer (or a plugin) adds the transaction data to the Data Layer (after a purchase is successfully completed)

- GTM is taught to recognize the successful purchase

- GTM (with help of Universal Analytics tag) transfers that data from the Data Layer to Google Analytics

Below is the GA Ecommerce dataLayer.push code. Most of the parameters are optional. Only *transactionId* and *transactionTotal* are necessary.

```html
<script>
window.dataLayer = window.dataLayer || [];
dataLayer.push({
 'event': 'purchase',
 'transactionId': '1234',
 'transactionAffiliation': 'Acme Clothing',
 'transactionTotal': 38.26, 
 'transactionTax': 1.29,
 'transactionShipping': 5,
 'transactionProducts': [{
   'sku': 'DD44',
   'name': 'T-Shirt',
   'category': 'Apparel',
   'price': 11.99,  
   'quantity': 1 
 },{
   'sku': 'AA1243544',
   'name': 'Socks',
   'category': 'Apparel',
   'price': 9.99,
   'quantity': 2
 }]
});
</script>
```

A few things to keep in mind:

1. The values of all the parameters must be replaced dynamically by the function(s) written by the developer.
2. The names of those parameters and the entire structure of the code must be identical to Google’s documentation.

### Where to place that code

In order to know where that dataLayer.push code must be added, first you need to think more about what happens after a successful purchase:

- Is the client redirected to a “Thank you” page?
- Or does the page remain as it is and only a “Success” message is displayed on the screen (but the URL of that page stays the same)?

If the client is redirected to a “Thank you” page, then that GA Ecommerce dataLayer.push code **must be placed above the GTM container code**. It’s very important to place it above. Why? Because then the Ecommerce transaction data will be already available for Google Tag Manager when it starts loading.

Some insights: The sooner that data is pushed to the Data Layer, the sooner you’ll be able to send this data to Google Analytics. Every time a page loads and GTM Preview and Debug mode is enabled, there are 3 events displayed there: *Pageview*, *DOM Ready*, and *Window Loaded*? If a developer places the GA Ecommerce dataLayer.push code above the GTM container, then you will be able to send the Transaction data to GA with the *Pageview* event. And that *Pageview* event is the earliest moment when you can fire tags.

If for some reason, a developer placed the Ecommerce dataLayer.push code below the GTM container, then the earliest moment when you can send that Ecommerce data to the GA will be *DOM Ready* trigger.

If the page does not reload when the purchase is successfully made, then your developer can place the code whenever he/she wants but one additional modification is needed then. A developer must add an additional parameter called “event” (its value can be whatever you want, e.g. “purchase”, “sale”, “ecommerce” or anything else that makes sense to you).

## GTM setup

Let’s remember those three scenarios from the previous chapter.

1. The Ecommerce dataLayer.push code is added **above** the GTM container (on a “Thank you” page)
2. The Ecommerce dataLayer.push code is added **below** the GTM container (on a “Thank you” page)
3. The Ecommerce dataLayer.push code is activated on **a page which is not reloaded** (after a successful purchase)

Depending on your project’s/website’s specifics you’ll have to choose one of these scenarios and create a trigger respectively.

### above

Trigger type: **Page View**
This trigger fires on: *Some Page Views*
Fires on: Page URL contains */order/purchase-successful/*

### below

Trigger type: **Page View - DOM Ready**
This trigger fires on: *Some DOM Ready Events*
Fires on: Page URL contains */order/purchase-successful/*

### not reloaded

Trigger type: **Custom Event**

A purchase is made → purchase event is pushed into the Data Layer → GTM catches that event and uses it as a Custom Event trigger → the trigger fires a tag which sends the data to Google Analytics.

# Prevent duplicate Transactions

If a customer lands on a “Thank you” page and refreshes it after a while, most probably, the GA Transaction tag will fire once again, which can cause duplicate orders and inflated numbers in your Ecommerce reports.

There are two solutions:

1. Ask a developer to fire the dataLayer.push code only once. If the page is reloaded, that shouldn’t be done again. This solution is **the most robust**.

2. Store order IDs in the cookie. And when the “Thank you” page is reloaded, GTM will check the cookie. If the cookie already contains the order ID of the current “Thank you” page, the Transaction tag is blocked.

# References

https://www.analyticsmania.com/post/ecommerce-tracking-with-google-tag-manager/