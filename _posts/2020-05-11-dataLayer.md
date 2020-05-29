---
title: "Google Tag Manager dataLayer"
date: 2020-05-11
tags: [Google Tag Manager, dataLayer]
header:
image:
excerpt: "Digital Analytics"
toc: true
toc_label: "Table of Contents"
toc_sticky: true
toc_icon: "cog"
---

# Intro

The dataLayer is one of the key concepts in the world of Google Tag Manager. It ensures maximum flexibility, portability, and ease of implementation. Understanding and leveraging the data layer is the key to unlocking GTM’s potential.

# How does dataLayer work?

dataLayer is a JavaScript array of objects that temporarily stores the data you need and then Google Tag Manager uses that data in tags, triggers, and variables 

# How to implement dataLayer?

There are two ways, how to add data to the Data Layer:

By adding a dataLayer snippet above the GTM container snippet. This is called “Data Layer declaration”
Or by pushing data with dataLayer.push method.

## dataLayer declaration

This method is not recommended. Because if ```dataLayer = []``` code snippet is added below the Google Tag Manager container code, then your entire GTM event tracking implementation will break (stop working). And this happens way too often.

## dataLayer.push

It’s very important that the Data Layer snippet is placed **above** Google Tag Manager’s container code in your website’s code. First, you need to send data to Data Layer, then this data is fetched by Google Tag Manager. If the snippet is placed after the GTM container code, dataLayer’s data won’t be fetched by Google Tag Manager.

Why is this method better than the first one? It can be placed anywhere in the code (above and below Google Tag Manager container) and it will not break the event tracking within GTM.

1. You have a newsletter signup form (which cannot be easily tracked with usual form tracking methods). You should ask your website developer to push a Data Layer event once a new subscriber has entered his/her email on your website. The code of this event should look like this:

```javascript
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  'event': 'new_subscriber',
  'formLocation': 'footer'
});
```

2. When a visitor adds a product to his/her cart, a Data Layer event (containing the product’s information) could be fired.

```javascript
window.dataLayer = window.dataLayer || []; 
window.dataLayer.push({ 
 'event': 'addToCart', 
 'products': [{
        'id': '123',
        'name': 'Black T-shirt',
        'brand': 'balenciaga',
        'quantity': 1
      }]
});
```

3. Also, with it, you can push events to the Data Layer that can be later used as triggering conditions. For example, if someone submits a form, a developer can activate the following code:

```javascript
window.dataLayer = window.dataLayer || []; 
window.dataLayer.push({ 
 'event': 'formSubmission' 
});
```

Since the code above contains the event key, this dataLayer.push can be used as a triggering condition in Google Tag Manager.

# How GTM uses dataLayer?

Google Tag Manager uses the information (stored in the dataLayer) in two ways:

1. To use certain pieces of data (in the shape of variables). 

2. To decide when to fire a tag (in the shape of triggers because you can use Data Layer events as triggers).

We can achieve the first part with the help of the Data Layer Variable and the 2nd one with triggers.

## Using the dataLayer variable

By default, Google Tag Manager does not recognize custom data in the Data Layer thus you cannot use it as variables. Unless you employ **the Data Layer Variable**. In order to create a variable, you’ll need to specify the Data Layer key of which value you want to retrieve. When the Variable is resolved, it will return whatever was most recently pushed into the key.

It’s important to remember that the “Data Layer Variable Name” field is **case sensitive**.

### Accessing various data structures in dataLayer

- Pulling data from child key: ```attributes.pagePostAuthor.someOtherKey```

```javascript
{
 attributes: {
    pagePostAuthor: 'Ivan Bu': {
       someOtherKey: 'example'
    }
 }
}
```

- Pulling data from array members: ```transactionProducts.0.price```

```javascript
window.dataLayer = window.dataLayer || [];
dataLayer.push({
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
```

In Javascript, if you want to pull the value of the first product’s price, you’d need to use transactionProducts[0].price (the index starts from 0), but Google Tag Manager does not support square brackets in this context, so you’d need to use dot notation, like this: transactionProducts.0.price.

### dataLayer variable Version

Another setting available in the Data Layer Variable is **Version**. When you select the Version, you’re instructing GTM to treat the values in the data model in two different ways.

- Version 1: It’s pretty limited and does not allow you to access nested values. That’s not the only limitation of Version 1. There’s also no merging available. Every time you push the data to the Data Layer, it will overwrite the entire key (that you’re pushing data to). 

So what’s the point of the 1st Version? It sounds like a useless thing, you might say. Definitely not. For example, in **Enhanced E-commerce**, it’s really important not to have any artifacts (scraps) from previous pushes, meaning that every time a window.dataLayer.push occurs, it rewrites keys.

- Version 2: the 2nd version is much more flexible. It allows you to access nested values, arrays, merge data.


## Using dataLayer in triggering

So once you reach the point where a developer pushes the interaction data (together with the event key) to the Data Layer, the next step is to catch that .push and turn it into a triggering condition. By default, Google Tag Manager does not care about the pushed events that are happening in the Data Layer (I mean that no tags will be fired unless you specifically instruct GTM to do so).

Since we are interested in tracking successful registrations, we need to tell GTM that registrationComplete events are important to us and we wish to use them as triggers.

In Google Tag Manager, go to Triggers and hit the New button. Choose Custom Event as trigger type and enter the Event name.


# Best Practices

1. Always use *dataLayer.push()*
2. Referencing the dataLayer within Custom HTML Tags: When GTM runs an Custom HTML tag, it appends the tags contents to the bottom of the document. This means Custom HTML scripts only run well after GTM is up and running; so you’re safe to reference the global dataLayer without instantiation within these tags.

```html
<script>
  (function() {
    
    dataLayer.push({
      'event': 'example'
    });
  
  })();
</script>
```  

# References

https://www.analyticsmania.com/post/what-is-data-layer-in-google-tag-manager/#declaration-vs-push

