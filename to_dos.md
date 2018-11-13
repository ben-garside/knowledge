[{"sap_id":"000000000030235788","price":32.4,"member_price":0,"non_member_price":0,"tax":6.48,"qty":1},{"sap_id":"000000000030303880","price":0,"member_price":54,"non_member_price":0,"tax":0,"qty":1}]
grep 7redg7uykvdko_stg2 /var/log/elasticsearch/elasticsearch.log.2018-04-16

================================================
The price of BS EN ISO 14001:2015 has changed. The price is £200.00. Click âComplete your Orderâ to proceed or contact us for more information.

============================================
DELETE FROM `7redg7uykvdko_stg2`.`cron_schedule` WHERE `schedule_id`='277447';
DELETE FROM `7redg7uykvdko_stg2`.`cron_schedule` WHERE `schedule_id`='278728';
DELETE FROM `7redg7uykvdko_stg2`.`cron_schedule` WHERE `schedule_id`='319396';

SQLSTATE[42000]: Syntax error or access violation: 1064 You have an error in your SQL syntax; check the manual that corresponds to your MariaDB server version for the right syntax to use near '(SELECT `queue_lock`.* FROM `queue_lock` WHERE (created_at <= '2018-10-14 04:00:' at line 1, query was: DELETE FROM (SELECT `queue_lock`.* FROM `queue_lock` WHERE (created_at <= '2018-10-14 04:00:22'))
=======================
TO DOs:

OBJECTMANAGER REMOVAL from Checkout:
/var/www/staging_local/extensions/Bsigroup/AccordionCheckout/src/Plugin/Magento/Quote/Model/Item/ConfigProviderPlugin.php


Codis Fiscali check
https://standards-storeqa.bsigroup.com/rest/default/V1/carts/mine/balance/remove ⇒ Called 2 times
savePaymentInformationAndPlaceOrder in vendor/magento/module-checkout/Model/PaymentInformationManagement.php ⇒ Complete Order Exception(https://github.com/magento/magento2/blob/2.1.5/app/code/Magento/Checkout/Model/PaymentInformationManagement.php#L71)
/var/www/staging_local/extensions/Netresearch/OPS/Plugin/PaymentInformationManagementPlugin.php

My error was occurring at "\vendor\magento\module-quote\Model\QuoteManagement.php" at the line $order = $this->orderManagement->place($order);


==============================

MY PENDING TASK LIST:
​Additional Ecom API call (SS-698, SS-1215, SS-1220)


Other Jira Defects:
SS-687, SS-690, SS-1164 (Need to analyse the issue after deploying magento patch for additional logging)
SS-1161: Regression issues for Pay By Invoice (To be checked on Staging branches - could not replicate on local)


Trello Defects related with Checkout and Ecom API: Automation board, functional defects


Ingenico setup on PPD (Only issue on PPD, working fine on all other branches including my local)


Performance improvement on Checkout: To analyse and remove unused scripts (knockout & jquery files), remove additional function calls


Ecom API suggestions/improvements mentioned by Yaqub & Business:
Codice Fiscale validation - 16 alphanumeric values only (exact 16 char)
Adjust basket total to be passed to Ecom API - exclude all non-SAP item prices from total (i.e. only include price of  'Standards', 'Books', 'Online Access')
Manipulate discount amount of Events and add as item discount in event item



-==========================================
Magento Reports:

Sales by Customer Services (Volume of traffic by channel)
SCR failures (end to end success/failure reporting) - Matt
Payment for standards and membership via Invoice

---------------------
Nitesh Kumar Singh: HDFC Lucknow
----------------------
Below is the admin detail:
https://standards-storeppd.bsigroup.com/admin​
Username: support_admin
Pwd: Suppo@12
-----------------------------
https://devqa-cdk55aq-7redg7uykvdko.eu.magentosite.cloud/customer/account/index/

Credentials:  
phani.tummala@tcs.com/ Phani@555 
subhrateja@rediffmail.com/Test@1234 
dash.joshita@tcs.com/Test@1234 
subhrateja.satapathy@tcs.com / Test@1234
========================
Promo Code additional API call change (discussed on 01 Oct 2018 - Yaqub/Azham/Tom):

On loading checkout page, invoke  E-Comm API (Verify) to get list price with BSI address
If there is a price mismatch between SCR and SAP price mismatch message displayed
Estimates: 	[Total: 12 PD]
Call OrderVerify on page load: 5 PD
Show price mismatch message on page load: 3 PD
Pass Promo code (with additional business logic as per ZPER/ZDIS) on Review Order API: 3 PD
Testing: 1 PD
========================
StoreQA
StorePPD => Payment (follow up with Ingenico)
<CodiceFiscaleNumber>

Priscilla: 

=========================
To check with Ingenico (on 02 Oct):
CFT-2018-548730: Setup Test Ingenico on PPD environment failed
CFT-2018-547856:
CFT-2018-542768 (Ingenico Payment Failed for Master Card - Payment Review)
CFT-2018-544051, CFT-2018-548730  [PPD ingenico setup]
CFT-2018-545846 [Save card details - https://standardsstoreproject.atlassian.net/projects/SS/issues/SS-520 ]


CFT-2018-548570 -> Payment info does not save every time

CFT-2018-549479 - Ingenico ePayments Failed (SS-1160)
CFT-2018-548104: 3D security issue (Done - Issue with Iframe Ingenico setting)
CFT-2018-549502- Ingenico Payment Status Issue#000444976: Payment Requested (9) - [Suspected Fraud]
CFT-2018-548911 // RE: Ingenico 3D secure Payment Failure

000444427: VAT not showing, misc issues:
CFT-2018-548600

CFT-2018-549058 - Email sent to customer for same order id on DEVQA and Staging (To follow up with Magento support - for Order increment id format change)
CFT-2018-547856 => Resolved (The tax information is available in Magento but not in your Ingenico back office (except other payment methods like Open Invoice))


==============
HDFC Bank: Mikku Kumari
0091-1167901801
========================
82.40.167.180  => my home IP
185.13.106.209 => Mobile
=========================

Deploy the patches on UAT:

Search patches (relevance etc.)
Ingenico latest Extension

=========================
TO check in Daily Catchup / Sukamal:

RE: SHOP- Address fields validation (Ask Sukamal to Take as CR - Richa mail ref)

JIRA Defect Meeting:
SS-1221 (To raise with Ingenico)

To discuss with SAP:
SS-1162 => <TaxationCountry> - DONE on 02 oct
SS-1221
SS-1233 => To verify with DWH data (02 Oct)

SS-1220
SS-1219

To check with Sanjib and Update:
SS-1210

TO CHECK WITH SHARAN:
SS-1217

MY DEFECT STATUSES:
SS-690 & 1164 => Magento ticket (401 error via Ecom API)
SS- 1177, 1168 => Payment Failed Ingenico (PHANI working on this)
SS-1181
SS-1213 => To check self (Order Should not be created to SAP if Failed in magento)
SS-1221 => To check self 

SS-1215, 1220 => Promo Code - to be taken up after Go-Live (Deferred ??)
SS-1166, 1213 => Italy: Codis Fiscali (CHECK 000444976 - follow up with Ingenico too):
	- Get Payment Method in /var/www/staging_local/extensions/Bsigroup/OrderExport/Model/Data/Quote.php
Enable review order only when Codice Fiscali value
SS-1214 => 


======================================================================

---------------------------------------------------
Ingenico transactions:
Payment reconciliation
Capturing payment failures

Tickets:
SS-1177, SS-1168, SS-1214 (Ingenico Payment Status)
---------------------------------------------------

SAP:
Payment reconciliation
VAT
Errors at checkout

Tickets:
SS-1221 (YAQUB: Only send total amount which is relevant to SAP - exclude events etc.)
SS-1215, SS-1220 - Promo Code Additional Call => Deferred?
SS-1166, 1213  (Italy Codis Fiscale)
---------------------------------------------------

DWH customer updates – Customer details not consistently being updated in Magento
Tickets:
SS-1233 (To confirm with Yaqub - company_name => Customer Name1)
---------------------------------------------------

YAQUB:
DWH
Brazil - codis fiscale


[membership discount on BASKET - Suvradip]
https://standardsstoreproject.atlassian.net/projects/SS/issues/SS-698

SS-1200: Effort to implement Postcode validation (Suvradip)
SS-1217: DWH feed for credit facility
======================================================================

 
Admin Login for Working environment:
Url: https://standards-storeqa.bsigroup.com/admin 
Username: ingenico
Password: e2usWjPTr
 
Customer Login:
Email: Sanjib.Das2@bsigroup.com
Password: P4FuuzU.RP
-------------------------------------------------------------------------------------------
Admin Login for Non-Working environment:
https://standards-storeppd.bsigroup.com/admin 
Username: ingenico
Password: e2usWjPTr
 
Customer Login:
Email: Sanjib.Das2@bsigroup.com​
Password: P4FuuzU.RP​

=================================

Current Tasks list is below:
​Additional Ecom API call (SS-698, SS-1215, SS-1220)
 
Other Jira Defects:
SS-687, SS-690, SS-1164 (Need to analyse the issue after deploying magento patch for additional logging)
SS-1161: Regression issues for Pay By Invoice (To be checked on Staging branches - could not replicate on local)
 
Trello Defects related with Checkout and Ecom API: Automation board, functional defects
 
Ingenico setup on PPD (Only issue on PPD, working fine on all other branches including my local)
 
Performance improvement on Checkout: To analyse and remove unused scripts (knockout & jquery files), remove additional function calls
 
Ecom API suggestions/improvements mentioned by Yaqub & Business:
Codice Fiscale validation - 16 alphanumeric values only (exact 16 char)
Adjust basket total to be passed to Ecom API - exclude all non-SAP item prices from total (i.e. only include price of  'Standards', 'Books', 'Online Access')
Manipulate discount amount of Events and add as item discount in event item
 


===================================
Ingenico Meeting:

To check for Redirecting back to Quote page 
-===================================

--------- Files to Deploy to UAT ----------
/var/www/staging_local/extensions/Bsigroup/AccordionCheckout/src/Model/Tax/Calculation/CalculatorFactory.php

--------- Files to Deploy to Staging3/DEVQA from UAT ----------
/var/www/bsi-uk/app/code/Address/Billing/Controller/Index/afteraddnewshippingaddress.php 

-------- Patches to Deploy on UAT ------------
MDVA-6616_EE_2.1.9_COMPOSER_v1.patch  [Customer_grid reindex issue]

-------- Patches to Deploy on Staging3 / DEVQA ------------
MDVA-6616_EE_2.1.9_COMPOSER_v1.patch  [Customer_grid reindex issue]


===================================
Debugging on Local:

15 Oct 2018:
modified:   extensions/Netresearch/OPS/Model/Config.php
modified:   extensions/Netresearch/OPS/Model/OpsConfigProvider.php

===================================
[16-Oct-2018 10:56:47 UTC] PHP Fatal error:  Allowed memory size of 1073741824 bytes exhausted (tried to allocate 4096 bytes) in /app/7redg7uykvdko_stg/vendor/magento/zendframework1/library/Zend/Db/Statement/Pdo.php on line 228
Aitoc issue:
========================================

To Check Later:
Why this below cron is running - Sajid?
batch_order_export_for_sap
============================

Staging 3 Domain Certificate expiry message in deployment:
 Environment certificates
      - certificate 5b16494: expiring on 2018-12-19 12:01:15+00:00, covering staging3-nf5kgsq-7redg7uykvdko.eu.magentosite.cloud
    
    W: Missing certificate for domain standards-storeqa.bsigroup.com.c.7redg7uykvdko.ent.magento.cloud



========================


Merge Basket issues (26 Sep 2018):
Scenario:
Add hard copy in basket - with login
Add hard copy in basket - without login
Basket Issue => Shows 2 line items for same product (one with member price and other item with non-member price)
=====================================

Whitelisted IPS:

All Environments:
Suvradip: 45.112.69.110  (18 Oct)
186.251.10.172: Priscila (PPD & UAT) - 21 Oct

Staging:
Justyna: 92.40.249.205  (16 Oct)

PPD:

Vikram Kakaria: 203.81.71.92  (18 Oct)
 77.67.63.226 (Mark - Inigenico)
Suvradip - 45.112.69.164  (20 oct), 45.249.81.130 (30 Oct)

Staging3: 77.67.63.226 (Mark - Inigenico)

Staging3:
70.112.14.175 - Magento support (https://support.magento.com/hc/en-us/requests/106662)


Thirdparty extensions:

Ingenico (Staging3 & Staging2):
24.134.12.49
85.232.25.153 - 85.232.25.158
===================================

SS-1160

===================================
Exception
Notice: Undefined variable: credit_amount in /var/www/dev/app/design/frontend/Bsi/Shop/Magento_Customer/templates/account/dashboard/info.phtml on line 177Elastic Search: Search does not show the specific type of product on Staging2
…………...
Azham:
Please pick a range of number, maybe 7xxx series, and use it to for all future magento error codes. Please inform CS and IPP support not SAP team. Thanks.

================
GDPR Customer data deletion (meeting with Azham/Tom on 20 Aug 2018):

How to hash-out Email in magento - change email address to random and check for all relationships?
Trigger hashing data manually from Admin -> Customer -> Delete (enable Editable fields)

===================

UAT Customers (Pwd: Tester123):
Emily.Williams@customer851.co.uk
Charlotte.Martins@customer851.co.uk


Pranabesh.kala@tcs.com
Happy345!


=====================================================
INGENICO Contact:
The number to call is 0203 147 4966 option 2 and ask to be put through to Ramilo.

Live Ingenico Account (password changed on 08 Aug 2018):
https://secure.ogone.com/Ncol/Prod/BackOffice/home/index?CSRFSP=%2fncol%2fprod%2fbackoffice%2fpassword%2fchange&CSRFKEY=A90733F03AA11BBBC2D28FC79EAB5850899BAE5B&CSRFTS=20180808123238&MenuId=4


Login as PSPId: BSIstandards
Password: 1}d2r]qHkjV

Live API User: BSIstandardsAPIUat
Pwd: 1}d2r]qHkV


Magento setting:
(Admin -> Sales -> Payment Services -> Ingenico)

Update below for Live ingenico:

Environment: Prod
API User: BSIstandardsAPIUat
Password: 1}d2r]qHkV
SHA-In: 0xRFFvKv0Gpnt882
SHA-Out: 0xRFFvKv0Gpnt882

===========================================================

Test account password: M2n1...@@
=====================================================

======================
GB622103205

To check Jira Issues:
https://standardsstoreproject.atlassian.net/browse/SS-687 [Unable to complete your order]
===========================================
StoreQA Admins:

test_editor1 /Aug@2018 
test_editor2 /Aug@2018 
===========================================
Customer Loging for Sprint 9 testing:

lewisstewart2009@gmail.com - Password12£
======================
https://staging-standards.bsigroup.com/admin/catalog/product/edit/id/15646/set/10/type/configurable/store/0/key/7655f2f0d7aa6841b89fc9e10aa9a4a5f03c38a610a1b0bf1f957440951b33a5/back/edit/ 
BS EN ISO 14001:2015

https://staging-standards.bsigroup.com/admin/catalog/product/edit/id/1495/key/7655f2f0d7aa6841b89fc9e10aa9a4a5f03c38a610a1b0bf1f957440951b33a5/ 
BS EN 2240-037:2010
======================

Staging site issues:
1384	default	0	general	

==============================
Done below changes on Local:

To make sublime text as a default editor:

Vim /usr/share/applications/defaults.list

text/x-php=sublime_text.desktop
text/x-phtml=sublime_text.desktop

===============================

Trello Boards:
https://trello.com/b/sax2HPo5/bsishop-functional-defect-tracker 

To deploy on Staging (all sites):

/var/www/dev/app/design/frontend/Bsi/Shop/Magento_Customer/templates/account/dashboard/info.phtml [take from Dev for $credit_amount]

/var/www/staging_local/extensions/Bsigroup/AccordionCheckout/src/Plugin/Magento/Quote/Model/SaveAddressCustomAttribute.php

**************************** Self To Dos (13 Aug 2018) ************************
Admin -> Order Create -> [Inform Azham]

Ecom API: OrderCreate(): Pass only relevant TOTAL AMOUNT - exclude unaccepted SAP product types.
Ecom API: Save Item wise tax for EVENT (PENDING)

Reduce calling of this function: addressForm().saveEvidence();

Allowed Countries (Restrict country from Bsigroup setting): This feature is not working now?

Ask Tom about below on Monday:
To show item-wise tax for Invoices, Events etc
https://standardsstoreproject.atlassian.net/browse/SS-1212 
VatRegistrationNumber => ASK FROM DEVI

Priscilla: home, permission
Ingenico PPD
Reply to Sharan

DEFECTS to CHECK:
https://standardsstoreproject.atlassian.net/browse/SS-1199
https://standardsstoreproject.atlassian.net/browse/SS-1212  [Phani to add VAT in outstanding invoice product then Saurabh to add in checkout]

Defects to be discussed with Sharan:
https://standardsstoreproject.atlassian.net/browse/SS-1200   [shipping address field limitation]

To check with Ingenico:
SS-1168, 1169, 1170 : Payment Review, 3DS, Why not set as ‘Failed’ in magento

Update the ticket:
https://standardsstoreproject.atlassian.net/projects/SS/issues/SS-1169
000433918: Italy order (Codis Fiscale)

https://standardsstoreproject.atlassian.net/projects/SS/issues/SS-547 [pranabesh]
https://standardsstoreproject.atlassian.net/projects/SS/issues/SS-1173
https://standardsstoreproject.atlassian.net/projects/SS/issues/SS-1201  [Pranabesh]

https://standardsstoreproject.atlassian.net/projects/SS/issues/SS-717 [Tom - wdn product]

To Check with Balel:



SELF to CHECK LATER:
https://standardsstoreproject.atlassian.net/projects/SS/issues/SS-1161 [PO number - sanjib]

With Devi: https://standardsstoreproject.atlassian.net/projects/SS/issues/SS-1154 

https://standardsstoreproject.atlassian.net/projects/SS/issues/SS-1164  [Complete order button]

Staging -> Export promo code - content staging  (https://support.magento.com/hc/en-us/requests/98373 - follow up on this ticket)


Check for PARTNER / PARTNER FUNCTION - add custom variables in checkout like VAT

0047229320 => Partner (Membership number) - working


SCR - Matt Issues:
https://staging-standards.bsigroup.com/pid-000000000030330199 [0 price]

Member Credit OrderCreate SAP (to check):
Order created : 000408727  (order entity id #408529)
000426340 

Event promo code
Magento Backend -> Create Order


To check on Monday:
[Done - to check] subhrateja.satapathy@tcs.com/Test@1234 [StoreQA -Pay by Invoice issue - Evidence data could not saved issue]

TO DO: check & Install Free Extensions:

https://github.com/magemojo/m2-ce-cron
/var/www/staging_local/app/code/MageMojo  [For Advanced Cron Setting]

php bin/magento module:enable MageMojo_Cron
php bin/magento setup:upgrade
php bin/magento setup:di:compile
php bin/magento setup:static-content:deploy

Or,
composer require magemojo/m2-ce-cron
php bin/magento module:enable MageMojo_Cron
php bin/magento setup:upgrade
php bin/magento setup:di:compile
php bin/magento setup:static-content:deploy



https://amasty.com/promotions-manager-for-magento-2.html 
/var/www/staging_local/app/code/Amasty/Rgrid  [Advanced Promo Code]

php bin/magento module:enable Amasty_Rgrid





--------------------------------------------
Disable Email Communication:
Store -> System -> Mail Sending Settings -> Disable Email Communications
--------------------------------------------
Deployment:
Comment below line on /extensions/Bsigroup/OrderExport/Model/VerifyRepository.php
// throw new CouldNotSaveException(__('Verified order data could not be saved! ' . $e));

-> Put my file from extensions -> restricted country (payment-mixin.js)

To enable Abondoned Cart Reminder on Staging:
Enable from Stores->BSIGroup Settings
Deploy crontab.xml file

=> Apply this patch for delete page issue in CMS Grid MDVA-13040_EE_2.1.8_COMPOSER_v1.patch

=> Checkout issues on StoreQA
=> Checkout DELIVERY ADDRESS issues (Subhrateja)
=> Event Promo code:
/var/www/dev/extensions/Bsigroup/AccordionCheckout/src/Model/Tax/Sales/Total/Quote/CommonTaxCollector.php

	=> Call Amasty Support for Extension Purchase Details
	=> CreateOrder APi call not working on staging
=> Checkout (Event discount, Payload member credit)

JIRA Defects:
https://standardsstoreproject.atlassian.net/browse/SS-528 
https://standardsstoreproject.atlassian.net/browse/SS-547 (export promo code)
https://standardsstoreproject.atlassian.net/browse/SS-546 (start/expiry promo)


	=> To override DISCOUNT block in Order Summary (right side bar:
https://magento.stackexchange.com/questions/190688/cart-price-rule-discount-description-does-not-displayed-on-cart-page-in-magento 

Template ref: /var/www/dev/vendor/magento/module-sales-rule/view/frontend/web/template/summary/discount.html 

[Later to dos:]
https://trello.com/c/n72tHE0B/206-sprint-9-preorder-product-observations-in-store-qa-1st-augp3 [BIP shows as Hard copy in Checkout - right side block

Issues to check:

BS ISO 15118-5:2018 (# 000000000030312677)   ⇒ Showing below error as ADDRESSES are not getting updated in case of adding this product to basket (check the payloads) but working for 000000000030360903.
We are unable carry out your request at the moment. Please contact our Customer Relations team quoting error number [216,219]. Telephone number +44 345 086 9001. 

"Notice: Undefined variable: credit_amount in /var/www/dev/app/design/frontend/Bsi/Shop/Magento_Customer/templates/account/dashboard/info.phtml on line 177"

Notice: Undefined index: is_membership_address in /app/7redg7uykvdko_stg/app/code/Address/Billing/Controller/Index/afteraddnewaddress.php on line 56  [PHANI]
Notice: Undefined variable: product_id_c in /app/7redg7uykvdko_stg/app/code/OrderImport/Migration/Controller/Index/Index.php on line 235  [Sanjib]


Occurred for lewis: on checkout  (Hint: Seems occurred when someone has logged in to this same user and placed order)
{"message":"%fieldName is a required field.","parameters":{"fieldName":"cartId"}}
lewisstewart2009@gmail.com - Password12£

************************************************************************************

My TO DOs (22 June 2018):
Search LHS filter count customization (https://magento.stackexchange.com/questions/141353/function-displaying-the-number-of-found-products-in-layered-navigation-filters-i)


****************************************************************************************************
LIVE TESTING:

bsiuattesting@gmail.com (Italy Italy - User 1): Shows error of Insufficient balance
Hint: Gets resolved when 
"IsCreditBlock": true => No credit facility (we can put additional check)
Phani: To check for 47545074 (User1): member credit facility deleted but not reflecting in magento
Pay By invoice is coming twice (leone’s defect)
****************************************************************************************************



Done changes for self debugging:
/var/www/dev/vendor/magento/zendframework1/library/Zend/Cache/Backend/File.php: 
Line #99: 'cache_dir' => 'var/cache',

Staging Issues to check:
[2018-05-31 13:51:06] report.CRITICAL: Magento\Framework\Exception\LocalizedException: The element 'product.info.options'
 already has a child with alias 'default' in /app/7redg7uykvdko_stg3/vendor/magento/framework/Data/Structure.php:611

2018/08/10 11:39:59 [error] 19190#0: *138537 open() "/app/7redg7uykvdko_stg/pub/media/catalog/productno_selection" failed (2: No such file or directory), client: 80.231.230.193, server: staging-standards.bsigroup.com, request: "GET /media/catalog/productno_selection HTTP/1.1", host: "staging-standards.bsigroup.com", referrer: "https://staging-standards.bsigroup.com/

CMS files for PPD:
app/design/frontend/Bsi/Shop/Magento_Catalog/templates/product/view/freedownload.phtml 

Checkout TO DOs (self):

Partner number changes for Ecom API:
/var/www/dev/extensions/Bsigroup/OrderExport/Model/Data/Order.php: #124 & 125
Also need to be done in Request.php

Move billing address form to shipping address:
https://magento.stackexchange.com/questions/189853/move-billing-address-form-to-shipping-address-page-in-magento-2-1/205532?utm_medium=organic&utm_source=google_rich_qa&utm_campaign=google_rich_qa

Basket Page loading issue:
/var/www/dev/app/design/frontend/Bsi/Shop/Magento_Checkout/templates/cart/cart_offer.phtml -> MUNL Pardot -> ga() event can cause the issue

====================================================================

For SPRINT 9 UAT:
Admin Configuration:

CMS Version control config

Exceptions (Staging3):

[2018-08-04 12:14:37] report.CRITICAL: Exception: Notice: Undefined variable: _product in /app/7redg7uykvdko_stg3/app/design/frontend/Bsi/Shop/Magento_CatalogWidget/templates/product/widget/content/grid.phtml on line 456 in /app/7redg7uykvdko_stg3/vendor/magento/framework/App/ErrorHandler.php:61
====================================================================

For Next UAT Drop 3:
→ Do not drop Search Relevance patch + Delete 8605


Pause Period (SPRINT 7) - Drop3:
Apply below patch for url-key update i.e. url rewrite issue:
MDVA-3971_EE_2.1.3_composer_v1.patch
Patch for Search Relevance Issue (https://support.magento.com/hc/en-us/requests/80150):
MDVA-8082_EE_2.1.10_v1_COMPOSER.patch  [DID NOT RUN]
MDVA-9750_EE_2.1.12_COMPOSER_v2.patch  [DID NOT RUN]
……………………………………
[Below did not run - pending with magento]
Please remove patch MDVA-8605
Then apply patch from the attachment.
After applying the patch, please clean cache and run full reindex

Patch adds 2 additional config settings in Admin > Store > Configuration > Catalog > Catalog > Search

Elasticsearch Minimum Should Match
Elasticsearch Minimum Score
…………………………………...


CMS Changes:
⇒ [04 Jun 2018 - Mohan]
	app/design/frontend/Bsi/Shop/Magento_Catalog/templates/product/view/addtocart.phtml
app/design/frontend/Bsi/Shop/Magento_Catalog/templates/product/view/freedownload.phtml
app/design/frontend/Bsi/Shop/Magento_Catalog/web/css/details.css

⇒ The "sidebox-without-bgcolour" class will be used for this feature. The necessary adjustment has been done in Magento_Theme/css/helppage.css.  (to update to PPD from storeQA)


SPRINT 8:
Change all crontab.xml timings to befor 11 AM so that it does not conflict with DB Backup daily cron
Sanjib New version upgrade cron: http://staging-standards.bsigroup.com/emailnotification/Index/productUpgradeNotification 
To check for justina’s 2 products:
https://staging-standards.bsigroup.com/admin/catalog/product/edit/id/1495/set/10/type/configurable/store/0/key/cadd22ad4967ee2763545932dbc9d15aa1a43f097efcea4bbfa60bb3639c8fc0/back/edit/ 
https://staging-standards.bsigroup.com/admin/catalog/product/edit/id/15646/set/10/type/configurable/store/0/key/7655f2f0d7aa6841b89fc9e10aa9a4a5f03c38a610a1b0bf1f957440951b33a5/back/edit/ 

Sprint 7:
Admin Configuration Changes:
→ Manage Stock: Disable as not needed for BSI:
Admin -> Catalog -> Inventory -> Stock Options -> Decrease Stock When Order is Placed = ‘No’
Admin -> Catalog -> Inventory -> Product Stock Options -> Manage Stock = ’No’

→ Admin -> Sales -> Tax -> Default tax Destination calculation -> Default Country -> United Kingdom

→ Admin -> Customer Attributes -> is_membership_address -> Show on Storefront -> Yes,    Also set….Forms to Use In -> Customer Account Address
→ Admin -> Customer Attributes -> prefix -> Manage Labels -> Default Store View -> Title  (earlier it was ‘Choose’)

→ Admin -> Shipping Methods -> select ‘Tablerate’
→ [Not needed] Admin -> AccordionCheckout -> General -> Default Shipping Method => ‘Tablerate’
→ Sales -> Tax calculation -> Row Total
→ Change camel case for Pay By Credit or Debit Card, Member Credit => Pay By Invoice


New Attributes:
Customer attribute:	search by ‘Member’ (eg: member_expiry)
	Product Attributes:
Withdrawn
Also Bought Products

Update Sajid’s SSO xml code on DEVQA, storeqa etc.
file:/dev/app/code/Bsi/Config/etc/config.xml
Admin -> Sales -> AccordianCheckout -> show items setting + Make this admin menu under Bsigroup
/var/www/dev/extensions/Bsigroup/OrderExport/Model/Data/Quote.php -> getProductAttributeValue(): CHANGE LOGIC TO GET SELECTED FORMAT VALUE of configurable product


CHECKOUT TO DOs:
[Self]
On Complete Order => Ingenico ePayments Payment failed"

→ Check Add New Billing Address: Undefined issue + take idea about postcode validation on Add new Billing

-> Check backtrace of Checkout Steps (review order becomes open when we click Edit address etc.)
-> check why $this->getConfig function is not working on :
	/var/www/dev/extensions/Bsigroup/EcomApi/Helper/Curl.php  -> exec()
	//curl_setopt($curl, CURLOPT_TIMEOUT_MS, 10000);
-> To check sometimes item_price becomes 0 on checkout as per below IF block - Ecom API price value)
/var/www/dev/extensions/Bsigroup/AccordionCheckout/src/Model/Tax/Calculation/AbstractAggregateCalculator.php  [line #268 - 275]
Notice: Undefined index: PDFFlag in /var/www/dev/app/design/frontend/Bsi/Shop/Magento_Checkout/templates/cart.phtml on line 60
Notice: Undefined variable: prodPubDate in /var/www/dev/app/design/frontend/Bsi/Shop/Magento_Sales/templates/order/info.phtml on line 78
book.pthml
/var/www/dev/extensions/Bsigroup/AccordionCheckout/src/view/frontend/web/js/view/billing-address.js
Line# 377: saveNewAddress() ----> to check why addres is not saving


To check the ADD NEW BILLING ADDRESS form field additions via:
/var/www/dev/extensions/Bsigroup/AccordionCheckout/src/view/frontend/layout/checkout_index_index.xml
[/var/www/dev/vendor/magento/module-checkout/view/frontend/layout/checkout_index_index.xml]
To remove TOOLTIP from ADD NEW BILLING ADDRESS -> Telephone field:
/var/www/dev/extensions/Bsigroup/AccordionCheckout/src/Plugin/ModifyCheckoutLayoutPlugin.php  → modifyShippingFields()




---------------------
Sprint6 Demo:

Deploy below patch from StoreQA:Changes to Admin Catalog Product Listing not showing updated attribute values saved via Edit Product

PATCH_MDVA-2959_EE_2.1.3_COMPOSER_v2.patch   [Deploy this on DEVQA and StoreQA, UAT] -- 10 Apr 2018 (Elastic Search: Search Results showing Blank Page on all Staging Sites)
[Ref: https://support.magento.com/hc/en-us/requests/75119]

MDVA-6108_EE_2.1.8_COMPOSER_v2.patch  [Deploy this on DEVQA and StoreQA]
600-MDVA-1351.composer.patch
[Ref: https://support.magento.com/hc/en-us/requests/73774] 

Update on DEVQA and StoreQA:
https://support.magento.com/hc/en-us/requests/76343 (GA disable issue)
http://devdocs.magento.com/guides/v2.1/cloud/project/project-patch.html#upgrade-to-ece-tools 


To Do Later:
[Self]
https://support.magento.com/hc/en-us/requests/13818 [check this ticket: DEVQA - Error 503 - Service Temporarily Unavailable]

→ SAJID: To prepare a HOLDING PAGE in Maintenance Mode (Pranabesh)
=> To CHECK LATER: Implement below ticket for retaining GA account setting
	https://support.magento.com/hc/en-us/requests/76343


Sprint 5 Demo (01 Mar 2018):

DevQA/app/code/NosearchQuery/BlankSearch/Block/Rewrite/Result.php" to Staging and QA
Keep this module under app/code/Customer
app/code/PasswordChange/ChangePass/Controller/Rewrite/Account/EditPost.php
Please update this line in Magento_Theme/layouts/default.xml at line no 9 in storeqa. The change is highighted in red.
<meta name="x_ua_compatible" content="IE=edge"/>
Apply latest magento patch (https://support.magento.com/hc/en-us/requests/70091):
MDVA_3586_2.1.5_v1.composer.patch

Sprint4 Demo (31 Jan 2018):
-----------------------------
- Hierarchy for Blocks (CMS)
- 
- Customer Service: 
	* Show Membership Number (create another customer attribute)
	* Address:
		Disable Member Address (read-only)
		Separate Billing and Shipping Address
	* (later) Store Credit -> to integrate with Membership Credit

QA5 Testing for Performance:
------------------------------------
	Magento_CacheInvalidate
	Magento_MysqlMq
	
	Magento_CustomAttributeManagement	 --> check if it is contrib module?

	Steps done:
	------------
	- Enabled Developer -> Javascript Bundling
	
	Steps to check: Issue with theme only
	- Exception #0 (Exception): Warning: get_headers(): This function may only be used against URLs in /app/app/design/frontend/Bsi/Shop/Magento_Catalog/templates/product/view/gallery.phtml on line 23
	
	-> C:\xampp\htdocs\mage_cloud_devqa\bsi-uk\app\design\frontend\Bsi\Shop\Magento_Catalog\templates\product\view\attributes.phtml
		var proxy = 'https://cors-anywhere.herokuapp.com/';  ==> Line #261  [ASK TEAM WHY IT HAS BEEN USED]
		
	==> MENTION LOOK INSIDE ISSUES TO TEAM:#
		get_headers()
		gallery.phtml
		lookinside & no preview both coming
	
======================================================================
QA2 testing:
	update core_config_data set value=1 where path like '%dev/static/sign%';  [NOT RUN]
	
- Block on sector page (Building & Material):
'Useful Resources'
- TO check on Staging:
	- Withdrawn products are showing on Category page  -> individual products
	- Sajid: Import products with status='withdrawn' -> change visibility of simple products (catalog when status 'withdrawn')
	- -1 issue on staging
	- INT is down
	=> Special price issue
	=> Mass update withdrawn product 
	
Staging To Dos for Sprint4 Deployment:
---------------------------------------
	Create CS Users from admin:
	php bin/magento admin:user:create --admin-user="lewis.stewart" --admin-password="Admin@123" --admin-email="lewis.stewart@bsigroup.com" --admin-firstname="Lewis" --admin-lastname="Stewart"
	
	
	php bin/magento admin:user:create --admin-user="martin.byron" --admin-password="Admin@123" --admin-email="martin.byron@bsigroup.com" --admin-firstname="Martin" --admin-lastname="Byron"
	
	maria.crehan@bsigroup.com
	php bin/magento admin:user:create --admin-user="maria.crehan" --admin-password="Admin@123" --admin-email="maria.crehan@bsigroup.com" --admin-firstname="maria.crehan" --admin-lastname="maria"
	
	elizabeth.collins@bsigroup.com
	php bin/magento admin:user:create --admin-user="elizabeth.collins" --admin-password="Admin@123" --admin-email="elizabeth.collins@bsigroup.com" --admin-firstname="Elizabeth" --admin-lastname="Collins"

	diana.wiafe@bsigroup.com
	php bin/magento admin:user:create --admin-user="diana.wiafe" --admin-password="Admin@123" --admin-email="diana.wiafe@bsigroup.com" --admin-firstname="Diana" --admin-lastname="Wiafe"
	
	steven.gibbs@bsigroup.com
	php bin/magento admin:user:create --admin-user="steven.gibbs" --admin-password="Admin@123" --admin-email="steven.gibbs@bsigroup.com" --admin-firstname="Steven" --admin-lastname="Gibbs"
	
	maria.ladeira@bsigroup.com
	php bin/magento admin:user:create --admin-user="maria.ladeira" --admin-password="Admin@123" --admin-email="maria.ladeira@bsigroup.com" --admin-firstname="Maria" --admin-lastname="Ladeira"
	
	nisha.vaid@bsigroup.com
	php bin/magento admin:user:create --admin-user="nisha.vaid" --admin-password="Admin@123" --admin-email="nisha.vaid@bsigroup.com" --admin-firstname="Nisha" --admin-lastname="Vaid"

	rachael.dufu@bsigroup.com
	php bin/magento admin:user:create --admin-user="rachael.dufu" --admin-password="Admin@123" --admin-email="rachael.dufu@bsigroup.com" --admin-firstname="Rachael" --admin-lastname="Dufu"

	rakhi.shah@bsigroup.com
	php bin/magento admin:user:create --admin-user="rakhi.shah" --admin-password="Admin@123" --admin-email="rakhi.shah@bsigroup.com" --admin-firstname="Rakhi" --admin-lastname="Shah"

	eric.koppitz@bsigroup.com
	php bin/magento admin:user:create --admin-user="eric.koppitz" --admin-password="Admin@123" --admin-email="eric.koppitz@bsigroup.com" --admin-firstname="Eric" --admin-lastname="Koppitz"


	


	ADMIN:
	------
	=> Reimport below product (having format and Published Date issue) - stuck in reindexing - 05 Feb 2018:
			BSENISO15223-1 : 2016
	
	- Map -> Google Map API Key
	- Create role 'Customer Service', create custom users
	- Go To Stores -> Other Settings -> Remove Other customer Groups
	
	Template File changes:
	
	Existing site's Google Analytics:
		Change ?UPI= to ?pid=...on footer_web.phtml, footer_mobile.phtml (gaCommonCodeLookInside, gaShopCodeLookInside)
	
	CMS:
	-------------
	[To Check Self]
	CMS Page Hierarchy - To disable the users to re-order folders
	- It is not possible to provide read-only access to the CMS Hierarchy - the user has full access natively, and you will have to customize your instance and add a new ACL in order to add such a restriction.
	
	Code Fixes:
	--------------
	In file: extensions/Bsigroup/AbandonCart/etc/crontab.xml
		Change:

		<schedule>*/10 * * * *</schedule>
		To:
		<config_path>abandon_cart/general/cron_expression</config_path>

	
	
	************ new to do (06 Feb 2018) ****************
	- Please remove following patches form m2-hotfixes directory as they are already included in the latest patch:
		MDVA-7673_EE_2.1.7_v1.composer.patch
		MDVA-7937_EE_2.1.8_COMPOSER_v1.patch
	- Deploy below new patches:
		MDVA-8605_EE_2.1.8_COMPOSER_v1.patch  [search multi-filter - #12599]
		MDVA_3586_2.1.5_v1.composer.patch  [#70091]
		
		
	- [27 Jan 2018] product detail page: String cuts for previ draft ver and interelationships --> [‎27/‎01/‎2018 15:57] Richa Rana: BS EN 60099-5:2013
	
	
***************************************************************************************************************************
	
Staging To Dos for Sprint3 Deployment:
---------------------------------------
	[CMS]
	-> Allow Banners to Shop Editor
	
	-> add more timeout for admin users (Config -> Advanced -> Admin -> Admin): Admin Session Lifetime (seconds), Lockout Time (minutes)
	-> - Enable more time for abondoned basket setting (SANJIB) -> Checkout section
		- Remove CMS Import/Export module, BSS Commerce

		-> check by enabling flat tables in QA3
		=> SEARCH (why success msg showing)
		=> SEARCH -> if we can change relevance sorting

	-> Check CMS queries (priscilla - eg: robots.txt) -> Assign permission for Admin -> Design -> SEO (Allow Robots.txt (General -> Design))
	
	=> Check for showing '100' records --> no results showing (SRIDHAR)
	=> check Debajyoti's logic for autocomplete -> remove code from Js

	=> SEND MAIL FOR STAGING UPDATE TO RICHA
	=> QA2 => for SPrint4 testing

-> TO deploy in Next Drop (Friday):
	-> update default case in QA3 in productPlugin.php file in sort module

	=> [2018-01-08 09:46:02] report.CRITICAL: Exception: Notice: Undefined variable: _product in /app/app/code/CustomProduct/CatalogWidget/view/frontend/templates/product/widget/content/top_products.phtml on line 148

	==> Sajid: ICS_code_new => data is not populated

	- Sajid to check why Published Date Weight (YEAR) is different in below:
		https://staging-standards.bsigroup.com/admin/catalog/product/edit/id/15712/key/d88b41d39a130aa2e92b9ddbb1b22deb763f859c3d80907b189ce84c16c45a2d/
	- [Done] Admin: Add Publisher, published_date for Subscriptions + Events + Free Products
	- Remove unused attributes from Searchable + weights
	
	-> SAJID:
		Show all titles coming from XML -> Main/Part (refer Matt's email on 05 Jan)
	
	-> Remove permissions (create new Role for BSI ADMIN -> assign min permissions)
	
	- MERGE JS
	- INT changes(eg: attributes.phtml)
	- [done] Patch for Autocomplete - to limit results as per the admin setting
	- [done] Patch for CMS Hierarchy issue, submenu disappears after we same parent CMS page
	
-> BSI Essential:
	Date is not proper (01/1970)
	Also, Price should be shown like ..From.. (Same for EVENTS)

	
	--------
	Send mail to MATT for SCR Data:
		Price is not there for 30214246.xml, 30286014
		
		Date not present for below:
		BS ISO/IEC 27003:2017
		BSENISO15223-1 : 2016
		ISO/DIS 45001.2:2017
	
*********** Redirection to New Magento Shop site ******************
	Yaqub suggestions:
		- Url rewrite of existing shop's product pages to magento
		- SEO -> 
		- Google Analytics scripts
	
************ Internal Tasks ***********
	- How to keep FAILED ORDERS in magento (eg: when payment gets failed)
	- CMS Page edit -> show Preview button

	- merge INT to DEVQA (both)
	- Check STOCK setting - to disable this setting from admin
	- To check - AUTO COMPLETE: for High Sale items, also for Recently Published
	
	Raise a ticket to cloud:
		Set Use Flat Catalog Category to “Yes.”
		Set Use Flat Catalog Product to “Yes.”

	==== IMP TO DO LATER =========
	Admin Changes are done:
	Azham’s suggestion: Publisher, Published_date attributes are there for remaining product types like Subscriptions + Events + Free Products (to be used for searching) – Date to be added by Marketing team

	TCS To Do for above: For manually updated products: To update the custom weight attributes when the above products gets updated – (eg: type_weight, publisher_weight, publication_date_weight etc.) – [to be done on after_save event for product save]

	
***************************************
	
--------------------
R & D:
	-> Can we add type weight as per the product type for all manually/DWH products eg: subscriptions?
--------------------

	
-> We're sorry, an error has occurred while generating this email.
-> deletion of manual products

-> chk with unmerged css/js
-> check app/code, extensions etc
-> pub/media from QA3 & INT

=> Delete manual products

=> Check existing users, customers => as per Sprint1 UAT sheet
=> apply patch for auto complete

-  atttributes.phtml: publisher_new => publisher
		published_date_new => published_date_weight
- Check GA Code (header.phtml), Admin GA setting

Update on INT/QA3 from staging:
	-> app/design/frontend/Bsi/Shop/Magento_Catalog/templates/product/view/freedownload.phtml
	-> Magento_Theme/header, footer_mobile, footer_web
	-> email_reminder/crontab.xml
	
	-> Registration.xml, theme.xml => push to Integration ( => merge Staging to Integration)

	
To Check: Member login => tier price


-------------------------------------------------------
Sample CMS Page Block (Eg: Latest Standards, Useful..]:
<div style="padding-top: 20px;">
<div class="navbox2">
<div class="block widget block-new-products list">
<div class="block-title"><strong>[Content to be added by Marketing team]</strong></div>
<div class="block-content">
<div class="products-list list"></div>
</div>
</div>
</div>
</div>

	......Old CMS block code for widget .......
	<p>{{widget type="CustomProduct\CatalogWidget\Block\Product\ProductsList" title="Featured Standards" collection_sort_by="created_at" collection_sort_order="desc" show_pager="0" products_count="3" template="CustomProduct_CatalogWidget::product/widget/content/top_products.phtml" conditions_encoded="a:2:[i:1;a:4:[s:4:`type`;s:50:`Magento|CatalogWidget|Model|Rule|Condition|Combine`;s:10:`aggregator`;s:3:`all`;s:5:`value`;s:1:`1`;s:9:`new_child`;s:0:``;]s:4:`1--1`;a:4:[s:4:`type`;s:50:`Magento|CatalogWidget|Model|Rule|Condition|Product`;s:9:`attribute`;s:17:`publicationstatus`;s:8:`operator`;s:2:`==`;s:5:`value`;s:2:`22`;]]"}}</p>
	...........................................
-------------------------------------------------------
Remove commercebug from unused environments like QA3
===================================================================
TO DO For SCR Import (Sajid):
	- Create Setup scripts for below:
		cross_links
		replaces_links
		
		Any mapping in core_config_data

TO DO In Next Drop:
---------------------
	- Update abandoned cart reminder template from QA2 to Staging
	- vi composer.json and add below line:
		"bsigroup/emailreminder": "^1.0",
		

##To do manually on Staging:
----------------------------
Mohan:
- Update cross-reference in product 'BS ISO 16343:2013'
- Update Pardot Forms

Saurabh:
==> Merge all changes of STAGING (SPRINT2) - URGENT
- Code change for mini-basket duration
- Set height of MUNL ifrmae to 650
- change GA account ID: UA-84364533-2
- Change JS file path for existing shop's GA script:
	<script src="/Resources/cookie/jscript/set-cookie.js"></script> - https://shop.bsigroup.com/Resources/cookie/jscript/set-cookie.js 
	<script src='/Resources/jscript/gaAddons.js' type='text/javascript'></script> -  https://shop.bsigroup.com/Resources/jscript/gaAddons.js
-----------------------------------------------------------------------------
#GA to check:
No Event fires upon submitting a MUNL form

---------------------------------------------

GA & Pardot script from OLD Shop (kept on Staging -- magento_theme/footer_web.phtml, footer_mobile.phtml):
-------------------------------------------------

<!-- @ToDo Later: Keep in Miscellaneous HTML in footer (Admin -> Content -> Configuration -> Store/website) -->
<!-- Pardot tracking script -->
<script type="text/javascript">
    var piProtocol = (("https:" == document.location.protocol) ? "https://pi." : "http://cdn.");
    document.write(unescape("%3Cscript src='" + piProtocol + "pardot.com/pi.js' type='text/javascript'%3E%3C/script%3E"));
</script>
<script type="text/javascript">
    piAId = '44652';
    piCId = '1154';
    piTracker();
    piAId = '74472';
    piCId = '1462';
    piTracker();
    piAId = '36972';
    piCId = '2434';
    piTracker();
</script>

<!-- Google Analytics tracking script (copied from old shop) -->
<script src="https://shop.bsigroup.com/Resources/cookie/jscript/set-cookie.js"></script>
<script type="text/javascript">
    var gaJsHost = (("https:" == document.location.protocol) ? "https://ssl." : "http://www.");
    document.write(unescape("%3Cscript src='" + gaJsHost + "google-analytics.com/ga.js' type='text/javascript'%3E%3C/script%3E"));
</script>
<script type="text/javascript">
    var gaCommonCode;
    try {
        gaCommonCode = _gat._getTracker("UA-7972162-1");
        gaCommonCode._setDomainName("none");
        gaCommonCode._trackPageview();
    } catch (err) {
    }

    function gaCommonCodeLookInside(pageId)
    {
        gaCommonCode = _gat._getTracker("UA-7972162-1");
        gaCommonCode._setDomainName("none");
        gaCommonCode._trackPageview("lookinside?upi=" + pageId);
    }

    function delayTrigger()
    {

    }

    function gaCommonCodeTriggerPageView(pageName)
    {
        setTimeout(delayTrigger, 1000);
        gaCommonCode = _gat._getTracker("UA-7972162-1");
        gaCommonCode._setDomainName("none");
        gaCommonCode._trackPageview(pageName);
    }
</script>
<script type="text/javascript">
    var gaShopCode;
    try {
        gaShopCode = _gat._getTracker("UA-7970902-2");
        gaShopCode._setDomainName("none");
        gaShopCode._trackPageview();
    } catch (err) {
    }

    function gaShopCodeLookInside(pageId)
    {
        gaShopCode = _gat._getTracker("UA-7970902-2");
        gaShopCode._setDomainName("none");
        gaShopCode._trackPageview("lookinside?upi=" + pageId);
    }

    function delayTrigger()
    {

    }

    function gaShopCodeTriggerPageView(pageName)
    {
        setTimeout(delayTrigger, 1000);
        gaShopCode = _gat._getTracker("UA-7970902-2");
        gaShopCode._setDomainName("none");
        gaShopCode._trackPageview(pageName);
    }
</script>
<script language="javascript">
    var pageTracker = 'gaCommonCode,gaShopCode';
</script>
<script src="https://shop.bsigroup.com/Resources/jscript/gaAddons.js" type="text/javascript"></script>
<script type="text/javascript">
    var appInsights = window.appInsights || function (config) {
        function s(config) {
            t[config] = function () {
                var i = arguments;
                t.queue.push(function () {
                    t[config].apply(t, i)
                })
            }
        }
        var t = {config: config}, r = document, f = window, e = "script", o = r.createElement(e), i, u;
        for (o.src = config.url || "//az416426.vo.msecnd.net/scripts/a/ai.0.js", r.getElementsByTagName(e)[0].parentNode.appendChild(o), t.cookie = r.cookie, t.queue = [], i = ["Event", "Exception", "Metric", "PageView", "Trace"]; i.length; )
            s("track" + i.pop());
        return config.disableExceptionTracking || (i = "onerror", s("_" + i), u = f[i], f[i] = function (config, r, f, e, o) {
            var s = u && u(config, r, f, e, o);
            return s !== !0 && t["_" + i](config, r, f, e, o), s
        }), t
    }({
        instrumentationKey: "51537c52-92d9-4ace-8c70-2398d8c385e1"
    });

    window.appInsights = appInsights;
    appInsights.trackPageView();
</script>
=============================================

To Run on Localhost:

Temporary table created to resolve issue after updating from Sprint 9 (DEV branch):
CREATE TABLE dev.`catalog_product_entity_date` (
  `value_id` int(11) NOT NULL AUTO_INCREMENT COMMENT 'Value ID',
  `attribute_id` smallint(5) unsigned NOT NULL DEFAULT '0' COMMENT 'Attribute ID',
  `store_id` smallint(5) unsigned NOT NULL DEFAULT '0' COMMENT 'Store ID',
  `row_id` int(10) unsigned NOT NULL COMMENT 'Version Id',
  `value` datetime DEFAULT NULL COMMENT 'Value',
  PRIMARY KEY (`value_id`),
  UNIQUE KEY `CATALOG_PRODUCT_ENTITY_DATE_ENTITY_ID_ATTRIBUTE_ID_STORE_ID` (`row_id`,`attribute_id`,`store_id`),
  KEY `CATALOG_PRODUCT_ENTITY_DATE_ATTRIBUTE_ID` (`attribute_id`),
  KEY `CATALOG_PRODUCT_ENTITY_DATE_STORE_ID` (`store_id`),
  CONSTRAINT `CATALOG_PRODUCT_ENTITY_DATE_STORE_ID_STORE_STORE_ID` FOREIGN KEY (`store_id`) REFERENCES `store` (`store_id`) ON DELETE CASCADE,
  CONSTRAINT `CAT_PRD_ENTT_D_ATTR_ID_EAV_ATTR_ATTR_ID` FOREIGN KEY (`attribute_id`) REFERENCES `eav_attribute` (`attribute_id`) ON DELETE CASCADE,
  CONSTRAINT `CAT_PRD_ENTT_D_ROW_ID_CAT_PRD_ENTT_ROW_ID` FOREIGN KEY (`row_id`) REFERENCES `catalog_product_entity` (`row_id`) ON DELETE CASCADE
) ENGINE=InnoDB DEFAULT CHARSET=utf8 COMMENT='Catalog Product Datetime Attribute Backend Table';
=============================================

Tharunraj Kr (4 Yrs Magento, 2.5 PHP):

Result: Failed
Rating: 2/5
Comment: Need improvement (worked on Magento 1.9, 3 months Magento 2.x, Theme customisation, basic custom module development)

Interview taken on 29 Oct (Sat):
----------------
Srijith S (6 month php, 6 yrs magento, 1 yr Magento 2):

Result: Passed
Rating: 3/5
Comment: Knowledge in Magento 1.x & 2.x, have experience in Migration.

----------------
Sreedarsh.A (5 Yrs total, 3 Yrs Magento - 1.9):

Result: Passed
Rating: 3.5/5
Comment: Good knowledge in Magento 1.x, checkout customisation, have worked on API integrations
