# EEC-dataLayer-Builder-for-GA4
**Do you use Enhanced Ecommerce Object of Google Universal Analytics in your dataLayer?**
Well, this variable is a smart way to track the GA4 Ecommerce (items).

If you have tracked this:

https://developers.google.com/tag-manager/enhanced-ecommerce

than this it will be the output:

https://developers.google.com/tag-manager/ecommerce-ga4

All custom dimensions and metrics are supported

## All EEC Events and EEC Object are automatically converted to GA4 Ecommerce Events and Object

In the table below all EEC UA Events are converted to GA4 Events
- green: is completely automatic
- yellow: you have to set up the number of checkout
- red: there is no possibility to convert in GA4 (it doesn't exist in Google Universal Analytics)

![events: e-commerce from universal google analytics to google analytics 4](https://www.tagmanageritalia.it/GTM/guida/uploads/2020/11/ecommerce-from-universal-google-analytics-to-google-analytics-4.png)



## The configuration: 
All you need it's just create 
- 2 custom template variables (EEC dataLayer Builder for GA4)
- 7 Data Layer Variables
- 2 custom event triggers 
- 2 GA4 Event Tags 

# Create EEC dataLayer Builder for GA4 variables:
## GA4 - Event Name
Create **"GA4 - Event Name"** and choose **Mode > Event Name** your checkout step for view_cart, begin_checkout, add_shipping_info, add_payment_info 

- 1 = view_cart (by default is blank)
- 2 = begin_checkout (by default the step is 1)
- 3 = add_shipping_info (by default the step is 2)
- 4 = add_payment_info (by default the step is 3)

![Matteo Zambon - GA4 Event Name](https://www.tagmanageritalia.it/GTM/guida/uploads/2020/11/Matteo-Zambon-GA4-Event-Name.png)


## GA4 - Items
Create **"GA4 -Items"** and choose **Mode > Items**

![Matteo Zambon - GA4 Items](https://www.tagmanageritalia.it/GTM/guida/uploads/2020/11/Matteo-Zambon-GA4-Items.png)

# Create Data Layer variables

For the purchase, you have to create 7 Data Layer variables. These are the parameters: 

- transaction_id
- affiliation
- value
- tax
- shipping
- currency
- coupon

Why do you have this?
Because in the GA4 ecommerce object these parameters are outside the __items__ and you have to grab them and use them in the GA4 Tag.

- ecommerce.purchase.actionField.id
- ecommerce.purchase.actionField.affiliation
- ecommerce.purchase.actionField.revenue
- ecommerce.purchase.actionField.tax
- ecommerce.purchase.actionField.shipping
- ecommerce.currency
- ecommerce.purchase.actionField.coupon

![datalayer variable ecommerce for ga4 and google tag manager](https://www.tagmanageritalia.it/GTM/guida/uploads/2020/11/datalayer-variable-ecommerce-for-ga4-and-google-tag-manager.png)

# Create Custom Events Triggers

Now, you have to create 2 different custom event triggers:

- GA – EEC Events
- GA - EEC Purchase

## Trigger GA – EEC Events 

This trigger contains all custom events for EEC of Google Universal Analytics. In this example, I use WooCommerce and Duracell Tomi plugin.

This is the list of all custom events:

gtm4wp.addProductToCartEEC|gtm4wp.checkoutStepEEC|gtm4wp.productClickEEC|gtm4wp.productImpressionEEC|gtm4wp.promoClickEEC|gtm4wp.promoImpressionEEC


![GA EEC Events for Google Analytics 4 by Google Tag Manager](https://www.tagmanageritalia.it/GTM/guida/uploads/2020/11/GA-EEC-Events-for-Google-Analytics-4-by-Google-Tag-Manager.png)

Product Detail and Checkout step 1 are pushed without custom events in the dataLayer. Yea, it's so bad, but we will use another trigger "All Pages" to fix this problem

## Trigger GA – EEC Purchase

This trigger contains the custom event for the purchase action: gtm4wp.orderCompletedEEC


![GA EEC Purchase for Google Analytics 4 by Google Tag Manager](https://www.tagmanageritalia.it/GTM/guida/uploads/2020/11/GA-EEC-Purchase-for-Google-Analytics-4-by-Google-Tag-Manager.png)

# Google Analytics 4 Tags: GA4 – EEC and GA4 – EEC – Purchase

Now we can create 2 Tags Event (of course I hope you have the GA4 configuration Tag already)

# Tag GA4 – EEC

Create a new GA4 Event Tag, we will use: 

- variables: **{{GA4 – Event Name}}** and **{{GA – Items}}**
- triggers: **All Pages** and **GA – EEC – Events**

![Google Analytics 4 Ecommerce Events with Google Tag Manager - Matteo Zambon](https://www.tagmanageritalia.it/GTM/guida/uploads/2020/11/Google-Analytics-4-Ecommerce-Events-with-Google-Tag-Manager-Matteo-Zambon.png)

# Tag GA4 – EEC Purchase

Create a new GA4 Event Tag, we will use: 

- variables: **{{GA4 – Event Name}}** and **{{GA – Items}}**
- 7 variables dataLayer 
- trigger: **GA – EEC – Purchase**

![Google Analytics 4 Ecommerce Purchase Event with Google Tag Manager - Matteo Zambon](https://www.tagmanageritalia.it/GTM/guida/uploads/2020/11/Google-Analytics-4-Ecommerce-Purchase-Event-with-Google-Tag-Manager-Matteo-Zambon.png)

# Now Debug it :)

Ok, go to debug it :)

![debug preview tag assistant - google analytics 4 ecommerce in GTM](https://www.tagmanageritalia.it/GTM/guida/uploads/2020/11/debug-preview-tag-assistant-google-analytics-4-ecommerce-in-GTM-1536x754.png)

![debug GTM - GA4 Tag Ecommerce promo](https://www.tagmanageritalia.it/GTM/guida/uploads/2020/11/debug-GTM-GA4-Tag-Ecommerce-promo-1536x692.png)

![debug GTM - GA4 Tag Ecommerce promo - detail](https://www.tagmanageritalia.it/GTM/guida/uploads/2020/11/debug-GTM-GA4-Tag-Ecommerce-promo-detail.png)

Great, it works. Now we have to check the GA4 Hit sent. Change the GTM code:

![debug GTM - GA4 Tag Ecommerce change Tag assistant](https://www.tagmanageritalia.it/GTM/guida/uploads/2020/11/debug-GTM-GA4-Tag-Ecommerce-change-Tag-assistant-1536x630.png)

![debug GTM - GA4 Tag Ecommerce hit sent](https://www.tagmanageritalia.it/GTM/guida/uploads/2020/11/debug-GTM-GA4-Tag-Ecommerce-hit-sent-1536x547.png)

And what about the purchase?

![debug google analytics 4 purchase with google tag manager](https://www.tagmanageritalia.it/GTM/guida/uploads/2020/11/debug-google-analytics-4-purchase-with-google-tag-manager.png)

