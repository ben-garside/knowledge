
Read this (Common Errors in Magento2):
https://blog.amasty.com/fix-common-issues-magento-2/?utm_referrer=https%3A%2F%2Fwww.google.co.uk%2F


* nGInx Configuration File: /etc/platform/7redg7uykvdko_stg3/nginx.conf

* Log File to refer: /var/log/platform/7redg7uykvdko_stg/error.log  			[Suggested by cloud on #12599 on 26 Jan 2018]
/var/log/mysql/mysql-error.log
					
/var/log/platform/7redg7uykvdko_stg3/error.log
/var/log/platform/7redg7uykvdko_stg2/error.log

*****************************************
Log File Paths in Magento Cloud: https://support.magento.com/hc/en-us/articles/360000318834-Find-logs-on-Cloud-Integration-Staging-Production 



Elasticsearch Log: /var/log/elasticsearch/elasticsearch.log
New Relic Log File:
/var/log/platform/7redg7uykvdko_stg3/newrelic_php_agent.log 
Deployment Log file:  /var/log/platform/7redg7uykvdko_stg3/deploy.log


======================================================================
https://magentocommeng.slack.com/messages/DATHMMPT8/
Username: saurabh.verma@bsigroup.com
Password: M2n1shlko@

Workspace URL: magentocommeng.slack.com
==================================================================
Magento.com ID: MAG005199032

======================================================================

Magento Cloud Environment Specific Hints:

Magento Versions Support Lifetime:
https://magento.com/sites/default/files/magento-software-lifecycle-policy.pdf 

Magento Upgrade from 2.1.9 to 2.2.0:
https://community.magento.com/t5/Magento-2-x-Version-Upgrades/Upgrade-Migrate-From-Magento-2-1-9-to-Magento-2-2-0-GA/m-p/76123#M756 

To increase mysql disk space:  /var/www/bsi_qa4/.magento/services.yaml
mysql:
    type: mysql:10.0
    disk: 4096

https://support.magento.com/hc/en-us/requests/77475 

 
Magento Logging:
https://devdocs.magento.com/guides/v2.1/config-guide/log/log-magento.html
============================================================
Logging Database Activity:
https://devdocs.magento.com/guides/v2.1/config-guide/log/log-db.html 
First, change the default preference:
<preference for="Magento\Framework\DB\LoggerInterface" type="Magento\Framework\DB\Logger\Quiet"/>
To
<preference for="Magento\Framework\DB\LoggerInterface" type="Magento\Framework\DB\Logger\File"/>
After that, add the following block to configure file-based logging:
<type name="Magento\Framework\DB\Logger\File">
    <arguments>
        <argument name="logAllQueries" xsi:type="boolean">true</argument>
        <argument name="debugFile" xsi:type="string">log/db.log</argument>
    </arguments>
</type>

24 Oct 18: Done on localhost in: /var/www/staging_local/app/etc
-----------------------------------------------------------------------------------------------------------
To kill process when Deployment Takes time:
$ ps aufx
kill 2800
Take MySql Dump for tables including Triggers:
Hint: https://support.magento.com/hc/en-us/requests/96354
sed -e 's/DEFINER[ ]*=[ ]*[^*]*\*/\*/'
-----------------------------------------------------------------------------------------------------------------
Suggestion for IP Bocking config:
https://support.magento.com/hc/en-us/requests/100598 
Navigate to: Magento admin > Stores > Configuration > Advanced > System > Full Page Cache > Fastly Configuration
Create a Custom VCL Snippet
Create a Edge ACL List allowlist.
Re-test for allowed / blocked IPs
-----------------------------------------------------------------------------------------------------------------
Suggestion from Magento Support for mage-cache storage issue:
https://alanstorm.com/magento-2-uielements-local-storage-module/
Also, please review our Frontend Developer Guide for additional information.
https://devdocs.magento.com/guides/v2.1/frontend-dev-guide/bk-frontend-dev-guide.html


To get MysqlVersion:
C:\xampp\mysql\bin>mysql -h localhost -V
mysql>SHOW VARIABLES LIKE 'version';

To get Mysql disk space usage:
MariaDB [main]> SELECT table_schema "database_name", sum( data_length + index_length )/1024/1024 "Data Base Size in MB" FROM information_schema.TABLES GROUP BY table_schema;


To get total File System Disk Usage:
web@7redg7uykvdko-qa4-5rxefly--mymagento:~$ df -H


Mysql Table full error solution:
tmp_table_size = 64M / max_heap_table_size = 64M    in my.cnf file
https://magento.stackexchange.com/questions/118277/magento2-reindex-issue-mysql-configuration?answertab=active#tab-top 
=================================
Elasticsearch Synonym Issue (raised by Tom/Mike):
https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl-regexp-query.html [suggested by Cloud support]
https://www.elastic.co/guide/en/elasticsearch/reference/2.3/query-dsl-regexp-query.html 
https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl-minimum-should-match.html 

ElasticSearch Debugging:

To get all Clusters/Index info: curl 'localhost:9200/_cat/indices?v'

Search results not showing due to Disk Space issue (50GB total for all staging sites):
Ref: https://support.magento.com/hc/en-us/requests/83741 
Root cause was lack of disk space - /data/exports - e.g files. Because of this Elastic search could not run properly.
Reindex was required after Elastic search node went back up.

192.168.5.5 7redg7uykvdko root@i-026fcdaeb2a67a1ee:/var/log/elasticsearch# df -h /data/exports
Filesystem      Size  Used Avail Use% Mounted on
/dev/xvdi        69G   19G   50G  28% /data/exports


**************************************************************************
Ingenico:

Custom (Dynamic) Template in Ingenico (instead of using iframe):
https://payment-services.ingenico.com/int/en/ogone/support/guides/integration%20guides/e-commerce/payment-page-look-and-feel#dynamictemplate 

Save Card Details (Alias): [Refer email dated 13 June 2018]
Several things that needs to be mentioned if you wish to not show the message to have the card holder’s data saved or not. If it’s not there and you save it, it is not fair for your customers and you may have some gdpr issues. Another point that needs to be mentioned is that the more aliases you create and store the higher the costs will be, as we will charge you for your aliases.
 
This is of course only applicable for the live environment.

So if the box is ticked then the alias.storepermanently=Y and if it’s unticked then =N
 
As your configuration in the Back Office is to show this message the message comes on the payment page.
 

 
If you put this on No then the message above will not be shown and you will create an alias and store it permanently.

*******************************************************************************************************
Magento Team’s references (provided by Vishal sir on 18-May-2017):

Coding Standards
http://devdocs.magento.com/guides/v2.1/coding-standards/bk-coding-standards.html
 
Technical Guidelines
http://devdocs.magento.com/guides/v2.1/coding-standards/technical-guidelines/technical-guidelines.html
 
Testing
http://devdocs.magento.com/guides/v2.1/test/testing.html

Performance Improvement:
https://devdocs.magento.com/guides/v2.1/config-guide/prod/prod_perf-optimize.html 

Ref to more attached documents:
https://drive.google.com/drive/u/0/folders/1yMbKlqMZkJ8Q_dbzk4MHeeVtUGa9fzhx 
Or, https://drive.google.com/open?id=1yMbKlqMZkJ8Q_dbzk4MHeeVtUGa9fzhx 

----------------------- Login Credentials -------------------
http://www.magepsycho.com  (saurabh.verma@bsigroup.com - my….t) - created on 22 Apr 2018

--------------- Magento Team contact details (as in email) ------------------
Outi Greve
Channel Sales Director, Americas
Boston
Cell: +1-617.686.6692 – Skype: outi.greve1
*******************************************************************************************************

To get database etc. configuration details of magento environment (run below via SSH):
echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 -d | json_pp

**************************************************************************

To Run Elastic Search via console:
Staging:
curl -i -XGET '127.0.0.1:9200/'
curl -XGET 'http://127.0.0.1:9200/_count?pretty' -d '{"query": {"match_all": {}}}'


curl -i -XGET '250.0.66.197:9200/'
curl -XGET 'http://250.0.66.197:9200/_count?pretty' -d '{"query": {"match_all": {}}}'

curl -XGET 'http://250.0.65.47:9200/_count?pretty' -d '{"query": {"match_all": {}}}'

Cloud team suggestion to check product count:
 'curl -XGET localhost:9200/_cat/indices' 

---------------
Elastic Search Console for QA3:
	php -r 'print_r(json_decode(base64_decode($_ENV["MAGENTO_CLOUD_RELATIONSHIPS"])));'
	
	[Search Result - for 'quality']
	curl -XGET 'http://250.0.65.47:9200/_count?pretty' -d '{"query": {"multi_match": {"query" :"quality", "fields": ["_all"]}}}'
	
	[Search Analyser]
	curl -XGET '250.0.65.47:9200/_analyze?pretty' -H 'Content-Type: application/json' -d' {"analyzer" : "custom", "text" : "quality"}'
	

To fetch Memory Limit setting of cloud:
php -r "echo ini_get('memory_limit').PHP_EOL;"

+++++++++++++++++++++ Magento Cloud Credentials (INT) +++++++++++++++++++++++
web@7redg7uykvdko-int-g4h3wui--mymagento:~$  php -r 'print_r(json_decode(base64_decode($_ENV["MAGENTO_CLOUD_RELATIONSHIPS"])));'

=================================================================

Imp Links:
	Magento Books (Sajid):
	https://www.udemy.com
	https://mapt.packtpub.com

[Understanding]
	https://aionhill.com/how-many-products-can-magento-handle

	https://www.nucleussupport.com/magento  [Magento Paid Agency for Custom Magento Development - SUGGESTED BY CLOUD SUPPORT]
	https://www.packtpub.com/mapt/book/web_development/9781788298025/2
	
	https://www.mageplaza.com/kb/magento-2-demo.html  [Magento2 Demo]
	
	Sites for Page Speed:
	https://gtmetrix.com
	htp://pingdom.com
	Google Page speed
	
[Very Nice Magento Tutorial]
https://aionhill.com/how-many-products-can-magento-handle [Given by Vishal Sir on 08 Nov 18 -  tcs mail]

-----------------------------------------------------------
Sajid KT:
https://MageTalk.com 
https://udemy.com  (Take Magento Testing, Knockout Js from scratch, Mastering Knockout)
https://packtpub.com 


Ajax login controller from Checkout
/Users/sajidpatel/sites/BSI/magento2ce/extensions/Bsigroup/AccordionCheckout/src/Plugin/Magento/Customer/AjaxLogin.php

Static content redeploy: for ADMIN only:
php bin/magento setup:static-content:deploy --area=adminhtml --language en_US

Skills to Improve:
DevOps
Javascript
AWS Lambda, Hosting

.................................................................................
PDF upload via CMS: http://www.verticalrail.com/kb/magento-pdfs-media-library/
.................................................................................
Magento 2 Web API (Rest) Interfaces:
http://vinaikopp.com/2017/02/18/magento2_repositories_interfaces_and_webapi/ 
……………………..
https://magento.stackexchange.com/questions/122112/how-to-enable-pdf-on-wysiwyg-to-upload-attachments-to-products-on-magento-2
    https://blog.mdnsolutions.com/magento-2-enable-pdf-upload/
	https://github.com/magento/magento2/issues/9850

    https://github.com/experius/Magento-2-Module-Experius-WysiwygDownloads#markdown-header-change-log


    Go to a WYSIWYG-editor (for example in the content of a CMS Page or a product textarea attribute)
    Select a part of the text which is used as a Download Link (it is also possible to add the Download Link to an Image)
    Click on the 'Insert/Edit Link'-button (under the textformat dropdown, do not use the 'Insert/Edit Image'-button)
    Click on the 'Browse'-icon behind the Link URL-inputfield
    Select the Folder in which you want to upload the Downloadable File (recommended is to create a new Downloads folder to store all the Downloadable Files)
    Click the 'Browse files'-button
    Select the File from your Documents and click on the 'Open/Insert'-button
    Select the Uploaded File
    Click on the 'Insert File'-button
    (The 'File Upload'-windows will automatically close)
    It is recommended to set the Target to 'Open Link in a New Window)
    Press on the 'Insert'-button in the 'Insert/Edit Link'-popup
    The part of the text which was selected is now a Download Link for the selected file

To Unlink the Downloadable File just set the cursor on the Download Link and Click on the 'Unlink'-button.
.................................................................................

------------------------------------------
	To skip triggers from Mysqldump:
	mysqldump --skip-triggers
------------------------------------------

Local Magento2 Setup:

Setup PHP environment: https://www.digitalocean.com/community/tutorials/how-to-install-linux-apache-mysql-php-lamp-stack-on-ubuntu-16-04
Install/Setup supporting packages like Microsoft Azure Storage Explorer, phpmyadmin, FileZila, Meld, Mysql-workbench, sublime text
Go to /var/www and run below command to get local copy of code:
"git clone --branch staging 7redg7uykvdko@git.eu.magento.cloud:7redg7uykvdko.git staging"
Export and configure Database: Download a latest UAT copy from azure - scr/TCS-Internal-Dumps/db_dump_staging_sp9_uat_03Sep18_1524pm_wo_triggers.sql.gz
Change base_urls from core_config_data table after DB export
Change DB credentials in app/etc/env.php
Update php.ini settings as required for order migration
run "composer update"


Magento Import / Export:
*******************************************
	1) Order: $ 299.00	(https://www.aitoc.com/en/magento_2_orders_export_and_import.html)
		or, https://www.commerceextensions.com/dataflow-batch-import-export-orders-to-csv-magento-2.html
		[https://www.mageplaza.com/review/import-export-orders]
		

----------------------------------------------------------------------------------------------------


Custom Logging:
https://www.mageplaza.com/how-write-log-magento-2.html

MAGENTO DEPLOYMENT HINTS:

Deployment from Staging to Production:
https://devdocs.magento.com/guides/v2.1/cloud/reference/discover-deploy.html
https://devdocs.magento.com/guides/v2.1/cloud/live/stage-prod-migrate.html 

http://devdocs.magento.com/guides/v2.0/cloud/project/project-webint-snap.html

Follow these instructions for Staging and Production deployment: http://devdocs.magento.com/guides/v2.0/cloud/live/stage-prod-migrate-prereq.html 
and for static files and DB migration: http://devdocs.magento.com/guides/v2.0/cloud/live/stage-prod-migrate.html


Data & Configuration Migration: https://support.magento.cloud/hc/en-us/requests/11614

Deployment:                                                                                                                                                                                                                                                                                            
http://devdocs.magento.com/guides/v2.1/cloud/live/sens-data-over.html 

-----------------------------------------------------------------------
Solution for trigger issue during DB export (ERROR 1277 (42000) at line <number>: Access denied; you need (at least one of) the SUPER privilege(s) for this operation)
Solution:
mysqldump -h <database host> --user=<database username> --password=<password> --single-transaction main  | sed -e 's/DEFINER[ ]*=[ ]*[^*]*\*/\*/' | gzip > /tmp/database_no-definer.sql.gz
Hint: https://devdocs.magento.com/guides/v2.1/cloud/live/stage-prod-migrate.html 
----------------------------------------------------------------------------------------------------
Magento Maintenance Mode:
	php bin/magento maintenance:enable [--ip=<ip address> ... --ip=<ip address>] | [ip=none]
	php bin/magento maintenance:disable [--ip=<ip address> ... --ip=<ip address>] | [ip=none]
	php bin/magento maintenance:status
	http://devdocs.magento.com/guides/v2.0/install-gde/install/cli/install-cli-subcommands-maint.html
----------------------------------------------------------------------------------------------------
To install Magento CLI on Local (suggested by Magento in ticket #https://support.magento.com/hc/en-us/requests/85616):
https://devdocs.magento.com/guides/v2.2/cloud/before/before-workspace-magento-prereqs.html#cloud-ssh-cli-cli-install 

Enable Newrelic on Development branches (Note: Already enabled on Staging environments):
https://devdocs.magento.com/guides/v2.2/cloud/project/new-relic.html 

New Relic PHP Functions list: https://docs.newrelic.com/docs/agents/php-agent/php-agent-api 

Enclose these API calls in a conditional check for the PHP agent so that your code will work even if the agent is not present:
if (extension_loaded('newrelic')) {
  newrelic_set_appname($name);
}
Check NewRelic Status: https://status.newrelic.com/ 
===============================================================

Generate Code + DB backup in Magento:

Please provide me with a database dump and code archive so that I may investigate this issue further in our testing environment.
Magento 2.x:
In Magento 2 you can generate these dump files directly from the store admin. 
1) Go to System > Support > Data Collector
2) Click New Backup
3) Allow a few minutes to pass > click Refresh Status (may take longer, repeat every 5 minutes until completed). 
4) Relocate the generated dump files from the /var/support directory to the Magento root directory.
5) Provide the direct download link to the dump files (your store address and the file name as displayed)
https://youtu.be/KIHJvQKROXI
A video screen cast showing the steps to generate the dump files is also available at the following link:


===============================================================
Magento cloud commands:
To login to magento cloud via Terminal: magento-cloud auth:password-login

For project variables: magento-cloud pvget
For environment variables: magento-cloud vget
===============================================================
Magento Re-index:

Get list of re-indexer names:
	php bin/magento indexer:info

Unlock re-index process: https://magento.stackexchange.com/questions/126067/magento-2-how-to-unlock-reindex-process
	[Issue: Category Products index is locked by another reindex process. Skipping.]
	php bin/magento indexer:reset
	php bin/magento indexer:reset cataloginventory_stock
	
	php bin/magento indexer:status
	
	
	php bin/magento indexer:reindex
----------------------------------------------------------------------------------------------------

To Reset Customer Password from Database (Also check Admin -> BSIGroup Settings -> SSO -> ‘No’):
update customer_entity set `password_hash` = '7c6b5ddb4533988d2cc585dee0f81da4c47b08fada6bfd62661aac15abea633e:GbeCutpEntdRYPboBAjXc1zho17VbsyG:1' where email LIKE 'pt.user100@aol.co.uk';

To Activate the customers manually via DB:

UPDATE customer_entity SET rp_token=null, rp_token_created_at=null, confirmation=null WHERE 
email IN('du377797@gmail.com',
'Gabriela.Santos@customer851.co.uk',
'Yusuf.Bayraktar@customer851.co.uk',
'Amanda.Castelo@customer851.co.uk',
'Pierre.Moreau@customer851.co.uk',
'Charlotte.Martins@customer851.co.uk',
'John.Walker@customer851.co.uk',
'Emily.Williams@customer851.co.uk',
'Robert.Taylor@customer851.co.uk',
'Harry.Brown@customer851.co.uk',
'Kristoffer.Johansen@customer851.co.uk',
'Anastasia.Constantinou@customer851.co.uk',
'Klaus.Muller@customer851.co.uk',
'Valentina.Gonzalez@customer851.co.uk',
'Giuseppe.Ferrari@customer851.co.uk',
'Huang.YuYan@customer851.co.uk',
'Fernando.Rodriguez@customer851.co.uk',
'Molly.Daniels@customer851.co.uk',
'Markus.VanderBerg@customer851.co.uk',
'Olivia.Jones@customer851.co.uk',
'Patrick.Stevens@customer851.co.uk',
'Kelly.Murphy@customer851.co.uk',
'Thomas.Smith@customer851.co.uk',
'Stella.Larsson@customer851.co.uk',
'John.Lewis@customer851.co.uk');
----------------------------------------------------------------------------------------------------

+++++++++++++++++++++ Magento Cloud Credentials (INT) +++++++++++++++++++++++
To fetch Memory Limit setting of cloud:
php -r "echo ini_get('memory_limit').PHP_EOL;"

php -r 'print_r(json_decode(base64_decode($_ENV["MAGENTO_CLOUD_RELATIONSHIPS"])));'

----------------------------------------------------------------------------------------------------
Magento Debugging Guidelines (Developer modules):

Check maintenance mode is not Active and var/.maintenance.flag file does not exist
Run compilation commands (rename var/di and var/generation folders if required)
Check var/report/…. May be you error like below (Hint: Open setup_module table and update version as mentioned) : 
The following modules are outdated:
AllResults_AllAttributes schema: current version - 2.0.0, required version - 1.0.0
When setup magento on local:
1) Set base_secure_url, base_unsecure_url, Secure Base Link URL also
2) Run below command for Cache command not defined in namespace:
	bin/magento module:enable --all
bin/magento setup:di:compile


'Area code not set' issue in custom CLI commands in Magento 2
https://magento.stackexchange.com/questions/128658/magento-2-area-code-not-set-warning-in-3rd-party-module 
https://magento.stackexchange.com/questions/132940/area-code-not-set 
https://magento.stackexchange.com/questions/96747/area-code-not-set-issue-in-custom-cli-commands-in-magento-2 
----------------------------------------------------------------------------------------------------
NEW-RELIC Configuration:

Url: https://rpm.newrelic.com 
Username: saurabh.verma4@tcs.com
Pwd: M2n…@

New Relic Configuration (https://support.magento.com/hc/en-us/requests/85616):
https://devdocs.magento.com/guides/v2.2/cloud/project/new-relic.html 

Newrelic performance monitoring page:
https://rpm.newrelic.com/accounts/1729823/browser/99948856#/lite?percentile=50&_k=3cu6vl

Generate API Keys:
Account settings > Integrations > API keys
https://rpm.newrelic.com/accounts/1729823/integrations?page=api_keys 
https://docs.newrelic.com/docs/apis/rest-api-v2/getting-started/api-keys 

Insights API Key (To check):
https://insights.newrelic.com/no_accounts 
----------------------------------------------------------------------------------------------------

Mysql Debugging:

show full processlist;
-----------------------------------
Magento Log Files:
	/var/log/error.log  [server logs]

-----------------------
Common Issues:
-----------------------
o Service Temporarily Unavailable Magento 2 - the maintenance mode is enabled in Magento 2
	php bin/magento maintenance:status
	php bin/magento maintenance:disable  [DISABLE MAINTENANCE MODE]
		Or, Delete a file called var/.maintenance.flag in Magento root folder  [https://www.mageplaza.com/kb/service-temporarily-unavailable-magento.html]
=============================================
	
Magento CMS Bulk Import and Export ($25.99):
	http://shreejiinfosys.co.in/index.php/import-export-cms-page-block-magento-2.html
	
Magento SSO:
	https://github.com/uvdesk/Magento-2-SSO  [Free extension]
https://community.magento.com/t5/Just-Ask-Alan/Magento-2-OAuth-authentication-and-REST-API-access/td-p/22528
http://devdocs.magento.com/guides/v2.0/get-started/authentication/gs-authentication-oauth.html


CMS Page Control Paid extension:
https://plugin.company/magento2-extensions/cms-revisions.html


Magento2 extension to Add Robots setting on Product and CMS Pages:
https://redchamps.com/meta-robots-tag-per-page-magento-2-extension.html [£69.00]
----------------------------------------------------------------------------------------------------

Magento 2 CLI (Command Line): https://www.mageplaza.com/magento-2-command-line-interface-cli.html
.................................................................................#


Magento Site Improvements: https://inviqa.com/blog/magento-2-tutorial-site-performance-tips

----------------------------------------------------------------------------------
	Command suggested by Cloud team for analysing Performance of site (does not work from our side):
	ab -n5 -c1 https://qa2-dh6pqni-7redg7uykvdko.eu.magentosite.cloud/
		This is ApacheBench, Version 2.3 <$Revision: 1430300 $>
		Time per request:       814.380 [ms] (mean, across all concurrent requests)

Customer: Add Prefix (eg: Mr./Mrs/...):  Configuration -> Customer -> Name and Address Options
		
Enable Varnish Cache in Magento:
	http://devdocs.magento.com/guides/v2.1/config-guide/varnish/config-varnish-magento.html
	
	Go to STORES > Configuration > ADVANCED > System > Full Page Cache. Click the dropdown box of “Caching Application”. Choose “Varnish Caching” from the list.
	https://www.cloudways.com/blog/magento-2-varnish-setup/

	
Get DB credentials etc in Cloud (run below on SSH):
	echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 -d | json_pp
	
	
Debajyoti (Search extension to check - left side layered navigation filter):
	/app/app/code/CzoneTech/AjaxifiedCatalog
	

UPDATE core_config_data set value = 'mysql' where path='catalog/search/engine';
-- Or, INSERT INTO `dev`.`core_config_data` (`scope`, `scope_id`, `path`, `value`) VALUES ('default', '0', 'catalog/search/engine', 'mysql');

Then run below commands:
php -f bin/magento setup:upgrade
php -f bin/magento cache:flush
php -f bin/magento indexer:reindex
Troubleshooting:
Edit app/etc/config.php file:
'system' => 
  array (
    'default' => 
    array (
      'catalog' => 
      array (
        'search' => 
        array (
          'engine' => 'mysql'

---------------------------
Magento2 Performance Improvements:
Ref: https://github.com/magento/magento2/issues/2999
Magento 2 is not slow. Now you can make it fast following these steps.
Update Magento Version
Configure Memcached
Optimize Javascript and CSS
Use lightweight theme
Images Should be Fully Optimized
Server and System Requirements
Enable Varnish Cache
Enable Flat Categories and Products
Content Delivery Network
Bug-Free Extensions
---------------------------

Algolia - Another Good Search Engine (alternative to Elastic Search):
https://community.algolia.com/magento/doc/m2/getting-started/
$ composer require algolia/algoliasearch-magento-2
$ php bin/magento module:enable Algolia_AlgoliaSearch
$ php bin/magento setup:upgrade
$ php bin/magento setup:static-content:deploy
Run below command after installing a module:
$ bin/magento module:enable Foo_Bar
$ bin/magento setup:upgrade -q && bin/magento cache:flush -q



Magento2 Weighted Search:
------------------------
https://www.humcommerce.com/tutorial/search-in-magento-2/#weighted_search
What happens when a customer searches for “red jacket”? Does Magento give search results for products with “red jacket” in the product name or products with “jacket” in the product name or both?
You can specify which results you want to show first in search results. You can also show only those results which are related to a specific part of a search term. All you need to do is assign Weight to attributes which are enabled for catalog search.
Attributes with higher weight are displayed in search results before the ones with lower weight.
For example, a search for “red jacket” has two search terms – a Color attribute and a Description attribute. Say, the Color attribute has a search weight set to ‘5’ and the Description attribute has a search weight set to ‘1’. The results will display search results for “red” and not for the “description”.
	
ELASTIC SUITE WIKI: https://github.com/Smile-SA/elasticsuite/wiki

ELASTIC SEARCH OFFICIAL DEMO: http://demo.magento-elastic-suite.io/index.php/men/tops-men/hoodies-and-sweatshirts-men.html?size%5B0%5D=XS&size%5B1%5D=S
		eg: http://demo.magento-elastic-suite.io/index.php/men/tops-men/hoodies-and-sweatshirts-men.html?color%5B0%5D=Orange&color%5B1%5D=Yellow&price=52-75&size%5B0%5D=XS&size%5B1%5D=S
	
	https://www.wyomind.com/magento2/elastic-search-magento.html#demo [demo of elastic search - paid extension]
	
HOW TO CONFIGURE MAGENTO's SEARCH:
	https://www.magestore.com/magento-2-tutorial/magento-2-how-to-configure-catalog-search/

	Magento filter price slider configuration: https://github.com/Smile-SA/elasticsuite/wiki/Attribute-configuration

	To Show left side layered navigation filter:
	https://www.mageplaza.com/kb/how-to-configure-layered-navigation-with-filterable-attributes-magento-2.html
	https://www.magestore.com/magento-2-tutorial/magento-2-how-to-enable-layered-navigation/
	
	https://magento.stackexchange.com/questions/156794/how-to-display-swatches-on-homepage-magento-2  [using magento swatches:]
	
	Re-index for Search:
	php bin/magento indexer:reindex catalogsearch_fulltext catalog_product_attribute
	
Elastic Search:
	Analyser: https://www.elastic.co/guide/en/elasticsearch/reference/current/analysis.html
	
	http://solr-vs-elasticsearch.com/

	 To get elastic search configurations:
	 php -r 'print_r(json_decode(base64_decode($_ENV["MAGENTO_CLOUD_RELATIONSHIPS"])));'
	
	Implement phrase search (eg: "...") i.e. search for combination of words.
	 https://stackoverflow.com/questions/24795822/search-keyword-using-double-quotes-to-get-exact-match-in-elasticsearch

	Elastic Search: https://www.elastic.co/guide/en/elasticsearch/reference/2.4/query-dsl-minimum-should-match.html  (given by Support - https://support.magento.cloud/hc/en-us/requests/11387)
	Custom Elastic Search Extension: https://github.com/Smile-SA/elasticsuite
	CMS Page Elastic Search: https://github.com/Smile-SA/module-elasticsuite-cms-search
	
Magento2 Layered Navigation Extension (Free):
	https://www.manadev.com/layered-navigation-filters-multiple-select-magento-2
	Demo: http://m2-demo.manadev.com/multiple_select_layered_nav/women/tops-women/jackets-women.html
	

Solr Search Extension (Suggested by Cloud Support): https://github.com/platformsh/platformsh-magento2-configuration/blob/9af92227940630c54d049912192c1d751c8ee250/Platformsh.php

Elastic Search: 
	Try 14 days trial : https://www.elastic.co/
	https://www.elastic.co/guide/en/elasticsearch/reference/2.4/query-dsl-minimum-should-match.html  (given by Support - https://support.magento.cloud/hc/en-us/requests/11387)
	https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl-query-string-query.html
	
	PHP Elastic Search: https://github.com/elastic/elasticsearch-php

	--------------- Issue of Blank Search Result after ELastic Search Configuration -----------------
	Refer: https://support.magento.cloud/hc/en-us/requests/11387
	......................................
	Hint: Make the attributes as SEARCHABLE='NO' which are eg: INTEGER (eg: price, product_published_date, date)
	sql> select a.attribute_code, a.frontend_label, a.frontend_input, b.attribute_id from eav_attribute a inner join catalog_eav_attribute b on a.attribute_id=b.attribute_id where b.is_searchable=1 and a.frontend_input not in ('select', 'text', 'multiline', 'textarea', 'multiselect');
	
	Elastic Search worked after setting Searchable=No for below attributes (as mentioned on call in morning):
		-	product_published_date
		-	price
		-	date
	Also, searchable as 'No' for tax_class_id,
	......................................

Elastic Search Left Side Layered Navigation Filter - To Customize Count on LHS filter:
https://magento.stackexchange.com/questions/141353/function-displaying-the-number-of-found-products-in-layered-navigation-filters-i 
	
Elastic Search Issues (Drupal):
	https://www.drupal.org/files/issues/elasticsearch_connector-exception-thrown-when-searching-multiple-fields-2468133-9.patch
	
======================================================================
Magento Advanced Seach Module (magento 1): http://inchoo.net/magento/advanced-search-in-magento-and-how-to-use-it-in-your-own-way/
	
Layered Navigation SEARCH MULTIFILTER EXTENSION:
	Free:  https://www.manadev.com/layered-navigation-filters-multiple-select-magento-2
    https://www.mageplaza.com/magento-2-layered-navigation-extension/

    Demo (standard ext.): http://ln.demo.mageplaza.com/collections/performance-fabrics.html?style_bottom=106

https://www.mageplaza.com/magento-2-search-extension/

Global Search:
    https://magento.stackexchange.com/questions/128443/how-to-search-product-programatically-in-magento-2
    vendor/magento/module-search/Model/Query.php

    https://webkul.com/blog/how-to-use-search-criteria-in-custom-module/
    https://mage2.pro/t/topic/1121

    Demo for search:
        http://magento2demo.firebearstudio.com/catalogsearch/result/?q=Radiant+Tee+
        http://lnultimate.demo.mageplaza.com/catalogsearch/result/index/?q=Celeste%20Sports%20Bra&state=stock
		http://demostore2.neklo.com/product-position/women/tops-women/hoodies-and-sweatshirts-women.html?color=58&price=50-60

		
================= CLOUD SUPPORT PATCHES for Magento 2.1.8 ===========

1) Autocomplete Limit Search Results:  MDVA-3391_CE_2.1.2_COMPOSER_v1.patch
	https://support.magento.cloud/hc/en-us/requests/12640

2) [Deprecated by 8605] Elastic Search - Mismatching of Search results: MDVA-7937_EE_2.1.8_COMPOSER_v1.patch
	https://support.magento.cloud/hc/en-us/requests/12599

3) CMS Hierarchy Issue - Submenu disappears on page saving:  MAGETWO_67197.git-apply.composer.patch
	https://support.magento.cloud/hc/en-us/requests/12959

4) [Deprecated by 8605] Phrase Search - Search by "":  MDVA-7673_EE_2.1.7_v1.composer.patch
	https://support.magento.cloud/hc/en-us/requests/11387

5) [Deprecated by MDVA-9750_EE_2.1.12_COMPOSER_v3.patch] Mismatching of search result: MDVA-8605_EE_2.1.8_COMPOSER_v1.patch
	https://support.magento.cloud/hc/en-us/requests/12599
6) Fatal error while running re-indexing for 'Catalog Search index' (PHP Fatal error: Uncaught TypeError: DateTime::__construct() expects parameter 1 to be string, array given in /app/7redg7uykvdko_stg/vendor/magento/module-elasticsearch/Model/Adapter/FieldType/Date.php:61):
	MDVA-7888_EE_2.1.9_COMPOSER_v1.patch
	https://support.magento.cloud/hc/en-us/requests/14529

7) Special Character patch: https://support.magento.com/hc/en-us/requests/70091
	MDVA_3586_2.1.5_v1.composer.patch	
	
Hint (cloud file where patch goes):  /app/vendor/magento/magento-cloud-configuration/src/Magento/MagentoCloud/../../../../../../m2-hotfixes/MDVA-3391_CE_2.1.2_COMPOSER_v1.patch
	
8) [Still Pending] Elastic search relevance issue: https://support.magento.com/hc/en-us/requests/88802?page=1 
Please remove patches: 
MDVA-8605_EE_2.1.8_COMPOSER_v1.patch 
MDVA-9750_EE_2.1.12_COMPOSER_v2.patch
MDVA-9750_EE_2.1.12_COMPOSER_v3.patch
And apply new MDVA-9750_EE_2.1.12_COMPOSER_v4.patch 

9) MDVA-11197_EE_2.1.8_COMPOSER_v1.patch

10) Patch for Improving Re-indexing Speed (given along with Elastic Search Relevance issue):
https://support.magento.com/hc/en-us/requests/80150 
MDVA-6491_EE_2.1.9_COMPOSER_v1.patch


Patch for Add to Basket GA event: MDVA-4922_EE_2.1.4_COMPOSER_v1.patch [https://support.magento.com/hc/requests/96924]
Apply this patch for delete page issue in CMS Grid MDVA-13040_EE_2.1.8_COMPOSER_v1.patch
[Sanjib raised ticket]  Customer import getting failed due to validation check:
https://support.magento.com/hc/en-us/requests/97633 MDVA-3654_2.1.4_composer.patch
All Staging sites are down - 503 error (cron_schedule table lock issue)
https://support.magento.com/hc/en-us/requests/97693 
MDVA-4807_2.1.6_v1.composer.patch
Reindexing speed improver patch:
https://support.magento.com/hc/en-us/requests/77042 [Old Ticket]
https://support.magento.com/hc/en-us/requests/102366 [Patch Again provided in this ticket]
MDVA-6108_EE_2.1.8_COMPOSER_v2.patch
Customer Delete from Backend - does not reflect on grid (Need to run customer_grid reindex)
https://support.magento.com/hc/requests/100775
MDVA-6616_EE_2.1.9_COMPOSER_v1.patch
Patch for Additional Logging when ‘Complete Order’ button stuck due to exception:
https://support.magento.com/hc/en-us/requests/97940?page=2 
MDVA-4352_2.1.6_composer_v1.patch
=======================================================

-------------
Creating Bundle product with a Configurable product:
https://community.magento.com/t5/Find-an-Extension-that/Configurable-Product-In-Bundle/td-p/334

	Magento 2(Paid - £299) - https://www.wizkunde.nl/magento-2-configurable-bundle.html
	Magento 1(paid - $159) - https://ecommerce.aheadworks.com/magento-extensions/flexible-bundle-product.html
	
	
--------------
MINI Cart Hints: eg: view-source:http://demo.magento-elastic-suite.io/index.php/sale/test-1.html?eco_collection=1

			<div class="block block-minicart empty"
             data-role="dropdownDialog"
             data-mage-init='{"dropdownDialog":{
                "appendTo":"[data-block=minicart]",
                "triggerTarget":".showcart",
                "timeout": "2000",
                "closeOnMouseLeave": false,
                "closeOnEscape": true,
                "triggerClass":"active",
                "parentClass":"active",
                "buttons":[]}}'>
            <div id="minicart-content-wrapper" data-bind="scope: 'minicart_content'">
                <!-- ko template: getTemplate() --><!-- /ko -->
            </div>
--------------
Disable Cache for a block (Sajid Patel):

	Try the following:
	<referenceContainer name="content">
				<block class="Magento\Checkout\Block\Onepage\Success" name="checkout.success" template="success.phtml" cacheable="false"/>
				<block class="Magento\Checkout\Block\Registration" name="checkout.registration" template="registration.phtml" cacheable="false"/>
			</referenceContainer>
	cacheable=”false”

	https://trellis.co/blog/magento2-fpc-hole-punching/

	Also see:

	https://github.com/magento/magento2/issues/6392

--------------
Magento Profile: https://marketplace.magento.com/  [saurabh.verma4@tcs.com   -   M...o - chk]

Magento 2 Extensions:
------------------------

Extension for CMS swatcher: https://github.com/zaibi099/Magento/tree/master/Pakgentors

https://plugin.company/magento2-extensions/cms-revisions.html

Install phpspreadsheet library in magento2 (advanced version of phpexcel):
{
  "repositories": [
    {
      "type": "vcs",
      "url": "https://github.com/PHPOffice/PhpSpreadsheet"
    }
  ],
  "require": {
    "PHPOffice/PhpSpreadsheet": "dev-master"
  }
}


Remove Sales and Customer Data:
https://magento.stackexchange.com/questions/55737/removing-all-old-sales-order-and-customer-data 
https://www.designhaven.co.uk/2014/08/cleanly-delete-orders-sales-customer-data-magento/ 
Cancel Orders older than 3 days:
https://magento.stackexchange.com/questions/161936/cancel-the-orders-which-are-older-than-3-days 
https://magento.stackexchange.com/questions/152806/magento-2-run-a-specific-cron-without-cronrun-cli-command/152812#152812 
Save Configurable product Custom Options:
https://magento.stackexchange.com/questions/186201/magento-2-creating-product-with-custom-options 


Magento2 Custom Widget Development:
http://inchoo.net/magento-2/magento-2-custom-widget/ 


Configurable Product Vs. Product with Custom Options
https://www.appseconnect.com/difference-between-product-custom-option-and-configurable-product-in-magento/ 
Url Rewrite in magento cloud:
https://docs.fastly.com/guides/conditions/using-conditions

Rewrite using VCL (https://support.magento.com/hc/en-us/requests/76064) :	http://devdocs.magento.com/guides/v2.1/cloud/configure/cloud-vcl-custom-snippets.html
https://docs.fastly.com/guides/vcl-snippets/
https://docs.fastly.com/guides/vcl/uploading-custom-vcl


To fetch Custom options based on product type in magento (Order Item’s selected attribute value):
https://hotexamples.com/examples/magento.sales.model.order/Item/getProductOptionByCode/php-item-getproductoptionbycode-method-examples.html -> buildItemName()


Magento2 Delete Orders: 
https://github.com/manishjoy/magento2-delete-orders 


Magento Coding Standards : https://inchoo.net/magento-2/magento-coding-standards/ 



================================================
Online Canadian Marketplace:
https://www.shopify.co.uk/
================================================
Post data to Microsoft Azure:
https://stackoverflow.com/questions/39241302/how-can-i-upload-the-blob-in-azure-using-the-shared-access-signature-using-php

Fetch Folder content from Azure:
https://cmtoshop.blob.core.windows.net/dwh?restype=container&comp=list&sv=2017-04-17&si=dwh-admin&sr=c&sig=QtPKuup2vOZ9%2FzSUSNVCdEyDx%2BqIFzMz96fWYNzs938%3D Or,
https://cmtoshop.blob.core.windows.net/scr/Delta?sv=2017-04-17&si=scr-read&sr=c&sig=ycfRLgsAxpZ9ZIRUNLoEBpq%2B2RdajZRMTbWdPKO2EYc%3D&restype=container&comp=list 

PHP Azure Library:
https://yourstory.com/2012/02/windows-azure-storage-for-php-developers/ 
================================================
Allow Adding PDF to WYSIWYG editor: https://github.com/magento/magento2/issues/9850

Integrate Elastic Search on Magento CE:
https://github.com/Smile-SA/elasticsuite 


Apply rewrite via Fastly (eg: .htaccess not there for nGinx - Ticket: #76064)
https://docs.fastly.com/guides/conditions/using-conditions 
Magento2: Custom Routing
http://inchoo.net/magento-2/routing-in-magento-2/ 
https://magento.stackexchange.com/questions/158798/how-to-rewrite-magento-catalog-search-url 


Magento2 DB tables as per Entity:
https://magento.stackexchange.com/questions/102936/magento-2-how-to-truncate-customers-products-reviews-and-orders-table 


Magento Cloud: DB Migration Troubleshooting
http://devdocs.magento.com/guides/v2.1/cloud/live/stage-prod-migrate.html#troubleshooting-the-database-migration 


Pro architecture | Magento 2 | Diff between Staging & Dev
http://devdocs.magento.com/guides/v2.1/cloud/architecture/pro-architecture.html#backup-and-disaster-recovery 


Magento2: Add another Search Engine
http://inchoo.net/magento-2/magento-2-add-solr-elasticsearch/ 


Microsoft Azure access using PHP:
https://azure.microsoft.com/en-gb/resources/samples/storage-blob-php-webapplication/ 
https://github.com/Azure/azure-sdk-for-php/
https://github.com/Azure/azure-storage-php 
https://github.com/Azure-Samples/storage-blob-php-webapplication 
	
Admin -> Orders: Adding Product filter:
https://ranasohel.me/2014/11/05/view-and-filter-product-sku-and-name-in-magento-sales-order-grid/ 

Magento2 Cron Scheduler:
	https://github.com/magemojo/m2-ce-cron  [CHECK THIS]


https://github.com/wyomind/cronscheduler 
https://github.com/shockwavemk/magento2-module-cron-schedule 
	https://github.com/magemojo/m2-ce-cron [IMPROVED  CRON - To check]
https://github.com/AOEpeople/Aoe_Scheduler [Magento 1.x]


Increase Mysql memory:
https://support.magento.com/hc/en-us/requests/73911?page=1 
Update .magento/services.yaml to increase the space allocated to mysql, redeploy and re-attempt the restore.

To track the error coming after setup:upgrade (i.e. verbose: -vvv):
bin/magento setup:upgrade -vvv


Magento Promo / Discount settings:
https://sherocommerce.com/magento-discounts-with-shopping-cart-price-rules/ 

* To show dynamic year in footer (eg: copyright info):
	http://help.ncrretailonline.com/article/adding-a-dynamic-year-to-the-copyright-notice-in-the-footer-area.html
	Select System (horizontal top menu) / Configuration.
	Go to the General section, and then click on the Design tab.
	Expand the HTML Head panel.
	Copy and paste the following in the Miscellaneous Scripts field:
	<!-- DYNAMIC COPYRIGHT YEAR IN FOOTER -->
	<script language="javascript" type="text/javascript"> var dateObject=new Date(); </script>
	Expand the Footer panel.
	Copy and paste the following in the Copyright field and modify as needed:
	&copy; <script type="text/javascript"> document.write(dateObject.getFullYear()); </script> by [YOUR COMPANY NAME]. All rights reserved.
	Save your changes.
	Clear the cache (System / Cache Management > Flush Magento Cache button)

* To update the Basket time for Anonymous user:
(Admin -> Web -> Default Cookie Settings) – 1 Day => 86400 seconds:
30 days -> 

[Free] Login as a Customer from Magento Admin: http://www.extensions.sashas.org/blog/magento-2-login-as-customer.html
Hint for localhost: No Commands defined in cache interface
/vendor/colinmollenhour/cache-backend-file/File.php  [Copy this folder from other project setup]
Clear all cache folders, provide 777 permission to pub/static, var/*
→ Sometime due to disk space on Staging -> so clean up disk space
	→ Sometime due to wrong syntax in any config file (eg: config.xml -> enclose special characters with <![CDATA[....]]> )
==========================================
To implement Custom Shipping Rate (how to override value of shipping cost):
https://magento.stackexchange.com/questions/186997/collect-order-total-inside-shipping-method 
https://magento2-blog.com/magento-2-change-shipping-costs-during-checkout/ 
https://github.com/magepal/magento2-custom-shipping-rate
https://www.linkedin.com/pulse/how-create-custom-shipping-module-method-magento-2-hasan 

Create shipping method in magento:
http://inchoo.net/magento-2/creating-a-shipping-method-in-magento-2/ 

Disable Free Shipping method:
http://www.amitbera.com/magento2-how-to-disabled-free-shipping-method-in-frontend/
================================================
Magento2 has option to set product based tax, refer to below. Hope this resolves out Invoice product taax issue:
​https://www.mageplaza.com/kb/how-to-setup-fixed-product-tax-magento-2.html

* Magento 2 Free community module for Force Login as Customer: 
		[Force your guest visitors to log in first (or register), before allowing them to visit your pages and catalog]
		https://marketplace.magento.com/bitexpert-magento2-force-customer-login.html
		Force your guest visitors to log in first (or register), before allowing them to visit your pages and catalog
		[hint: https://blog.bitexpert.de/blog/magento2-frontend-customer-force-login-module/]
	
--------------

* To override magento admin - How To Add Custom Tab And Field In Magento Backend:
	http://www.magebuzz.com/blog/how-to-add-custom-tab-and-field-in-magento-backend/

================================================
Changes to Admin Catalog Product Listing not showing updated attribute values saved via Edit Product:

https://support.magento.com/hc/en-us/requests/73774
Stores > Configuration > Advanced > Developer > Grid Settings and reverse the setting, 
================================================



* OAuth API Integration:
	http://devdocs.magento.com/guides/v2.0//get-started/create-integration.html

* To go back to previous page from current page (can be helpful - Need to check): https://www.mageplaza.com/review/import-export-orders/	https://www.commerceextensions.com/dataflow-batch-import-export-orders-to-csv-magento-2.html?utm_source=mageplaza&utm_medium=mageplaza&utm_campaign=mageplaza-review&utm_content=Import%20And%20Export%20Orders

* Magento polling with Q & A:
	https://searchcode.com/codesearch/view/45787772/  [Need to check this]

O To Run a specific Cron-job in  magento:
php bin/magento cron:run --group=import_products

O To run a cron job manually from the command line
composer require-dev n98/magerun2

O Configure Magento on local via cloud setup (remember magento 2.1.8 works with PHP 7.0.28):
Git clone all files from cloud branch, export DB from cloud and import on local. Change env.php for DB, remove redis, cache arrays from env.php
Or, use composer install
Or, use 

To disable search engine setting from DB (DID NOT RUN):
	Go to core_config_data: update ‘catalog/search/engine’ with ‘mysql’

* Magento Performance Monitoring:
	[Apache Jmeter on Magento cloud]
	https://github.com/magento/magento-cloud/tree/master/setup/performance-toolkit

* Magento Product Attributes: https://www.magestore.com/magento-2-tutorial/magento-2-product-attributes/

* Export attribute set, import products (to check):
https://github.com/sunel/Magento-Import-Export/blob/master/export_attribute_set.php

https://github.com/sunel/Magento-Import-Export

* GeoIP Integration:
	Also check Fastly configuration
	https://www.mageworx.com/wiki/magento-geo-ip/
	
* Fastly Configurations:

To increase Admin Timeout via Fastly:
Go to > Stores > Configuration > Advanced > System > Full Page Cache > Fastly > Advanced Configuration.
We recommend increasing the value for "Admin path timeout" up to 300-600seconds.
Please also note that you have to press 'Upload VCL to Fastly' to apply new settings after saving via Stores > Configuration > System > Advanced > Full Page Cache > Fastly Configuration > Upload VCL to Fastly > Upload.

	To increase timeout: http://devdocs.magento.com/guides/v2.2/cloud/configure/fastly-vcl-extend-timeout.html
	
Fastly team pointed out that your are not using optimal Fastly Origin Shield Location or do not have Origin Shield enabled at all.
The Fastly Origin Shield feature helps reduce load by having all POPs check with one POP (the shield) before request go to the origin. This can reduce the traffic that has to be served by the origin particularly when content is not in the page cache.
In general, Fastly’s recommendation is to use a POP that is close to the origin to be the shield. Your closest Shield Location islondon-uk, refer below link:
	http://devdocs.magento.com/guides/v2.2/cloud/access-acct/fastly.html#backend 

* IE11 - Open Intranet Sites in Compatibility view:
		https://docs.microsoft.com/en-us/internet-explorer/ie11-deploy-guide/fix-compat-issues-with-doc-modes-and-enterprise-mode-site-list

* Jquery:
	Open iframe in a popup: https://stackoverflow.com/questions/25781628/how-to-load-iframe-content-in-popup-div

* Magento 2 Custom-API (REST): http://inchoo.net/magento-2/magento-2-custom-api/
		http://inchoo.net/magento-2/magento-2-api/

==========================================================	
* Magento Paid Extension for CMS Version Control (suggested by Sajid):
	https://plugin.company/magento2-extensions/cms-revisions.html
	
==========================================================
Magento2 Product Import Export Extension (Purchased by Sajid):

You can contact at but not sure he can provide support: scottbolasevich@gmail.com

More details of extension below, you can send your query from here as well:
https://xtensiongalaxy.com/custom-bulk-product-import-export-with-tier-pricing-custom-options-configurable-and-bundle-pro.html
https://www.commerceextensions.com/magento-product-import-export-magento-2.html
==========================================================

* Magento Webservice - Like Chrome Postman Tool:  Magento SWAGGER extension
		
* Get URL params in Block:
	$params = $block->getRequest()->getParams();
		
* To Add separate Header on Checkout (app/design/...../magento_checkout/layout/checkout_index_index.xml):
	<?xml version="1.0"?>
	<page xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	  layout="1column"
	  xsi:noNamespaceSchemaLocation="urn:magento:framework:View/Layout/etc/page_configuration.xsd">
		<body>
			<move element="logo" destination="header-wrapper"/>
		</body>
	</page>
		
* How to user Helper in Controller and Block:
	https://magento.stackexchange.com/questions/92078/custom-helper-in-custom-module-in-magento-2

	Alternative to add helper in controller thru objectManager but not preferrable:
	$object_manager = \Magento\Core\Model\ObjectManager::getInstance();
	$helper_factory = $object_manager->get('\Magento\Core\Model\Factory\Helper');
	$helper = $helper_factory->get('\Magento\Core\Helper\Data');
	
	Or, $this->_objectManager->create('Company1\Module1\Helper\Data')->someMethod();
		
* Sample CMS Data module for CMS Import/Export understanding: 
	Free to check - https://github.com/magespecialist/m2-MSP_CmsImportExport

	[Below suggested by Cloud support team]
	https://magento.stackexchange.com/questions/124833/magento-2-export-import-cms-blocks-and-cms-pages
	
	https://github.com/magento/magento2-sample-data/tree/develop/app/code/Magento/CmsSampleData

* Module for Populating States for All Countries: https://packagist.org/packages/credevlabz/magento2-directory-indian-states
		composer require credevlabz/magento2-directory-indian-states

* Solution to fix RegionId is a required fix (known issue in magento): https://github.com/magento/magento2/issues/6261

Custom Module to fix regionId issue: https://github.com/EliasKotlyar/RegionFix

Free extension for managing regions for other countries in magento (DID NOT CHECK):
https://github.com/php-cuong/magento2-regions-manager

* Required parameter 'theme_dir' was not passed
	Solutions:
		Main: Check app/design/frontend/Bsi/Shop/registration.php, theme.xml
		chmod 775 -R pub/media/theme  [May Be]
		
* Solution for theme not loading on frontend:
	MariaDB [7redg7uykvdko_stg]> SELECT * FROM theme WHERE theme_id=4; 
		+----------+-----------+------------+-------------+---------------+-------------+----------+------+----------+ 
		| theme_id | parent_id | theme_path | theme_title | preview_image | is_featured | area | type | code | 
		+----------+-----------+------------+-------------+---------------+-------------+----------+------+----------+ 
		| 4 | 1 | Bsi/Shop | Bsi Shop | NULL | 0 | frontend | 1 | Bsi/Shop | 
		+----------+-----------+------------+-------------+---------------+-------------+----------+------+----------+ 
		1 row in set (0.00 sec)
		
	
		update theme set type='0' where theme_id=4;   //Actual: 1
		update core_config_data set value=0 where path='design/theme/theme_id';  //Actual: 1
		
		SELECT * FROM theme WHERE theme_id=4; //type=1
		SELECT * FROM core_config_data where path like '%theme%';
		
* Issue: Unable to retrieve deployment version of static files from the file system
	Solution: https://magento.stackexchange.com/questions/178565/strange-error-when-running-setupupgrade-after-module-installation
				UPDATE core_config_data SET value = 0 WHERE path = 'dev/static/sign';
				Or, INSERT INTO core_config_data VALUES (null, 'default' , 0, 'dev/static/sign', 0);
				
				select * from core_config_data WHERE path = 'dev/static/sign';


* Generate .ics file (Add to Calender):
	https://gist.github.com/jakebellacera/635416   [PHP Class]
	https://stackoverflow.com/questions/12739247/how-to-generate-ics-file-using-php-for-a-given-date-range-and-time
			http://web.archive.org/web/20120419230026/http://jamiebicknell.tumblr.com/post/413492676/ics-generator-php-class
	
	Generate ics file using jquery: http://blog.jainsiddharth21.com/2015/05/23/generate-and-download-ics-file-for-an-event-using-jquery/
	
	How to open Apple calendar automaticly when generating “.ics” file:
	header("Content-Type: text/Calendar");
	header("Content-Disposition: inline; filename=".time().rand(1,100).".ics");
	
	How to Open ical file in outlook etc: https://stackoverflow.com/questions/45799284/why-does-my-php-generated-ics-file-open-in-a-text-editor
	"It depends on the users browser's settings for what to do with a filetype and yes as Rob suggested the filetype will be determined by the mime type, so just creating a text file with ics data in it is not adequate. It must have a mime type of 'text/calendar' AND the user's browser must be set to open whatever calendar application they use."
	
** Magento Cloud Support Tikets:
-----------------------------------------
	To Update Data & Configuration changes from Integration to Staging:
	https://support.magento.cloud/hc/en-us/requests/11614
	
** Patches from Magento Cloud Support:
----------------------------------------
- Changes to Admin Catalog Product Listing not showing updated attribute values saved via Edit Product

   600-MDVA-1351.composer.patch
   Ticket: https://support.magento.com/hc/en-us/requests/73774 
- Search by "...." (phrase word search)
- Patch for Autocomplete - to limit results as per the admin setting
- Patch for CMS Hierarchy issue, submenu disappears after we same parent CMS page
	https://support.magento.cloud/hc/en-us/requests/12959
-Patch for Saving address twice (https://support.magento.com/hc/en-us/requests/83655):
 MDVA-6584_EE_2.1.9_v1.composer.patch
 Known issue in Magento 2.1: https://github.com/magento/magento2/issues/8181

Apply below patch for url-key update i.e. url rewrite issue:
MDVA-3971_EE_2.1.3_composer_v1.patch

** Reset Customer Password via cli:
	UPDATE customer_entity SET password_hash = 'd02b1b30ee945a1e4fb2d0880be280a9065ef172b871cbdbd364b98daa88c4e2:jwuOF5GRDLTtvEWJIqSIBSJKHlG7Pwrf:1' WHERE email='bsigerm.nm@aol.co.uk';
	
** Create new admin user:
	php bin/magento admin:user:create --admin-user="saurabhverma1" --admin-password="M2n1shlko@" --admin-email="admin@example.com" --admin-firstname="Saurabh Admin" --admin-lastname="Admin"
	
** BSI Add New billing address (middle_name=1 in customer_address_entity), middlename=0 for shipping address
	update customer_address_entity SET middlename=1 WHERE entity_id IN('305', '306', '307', '308') AND parent_id=36;
	select entity_id, is_active from customer_address_entity where parent_id=34;
	
** For customizing Order number: https://bsscommerce.com/magento-2-custom-order-number-extension.html  -> $159.00

	
** Save Customer Data Programatically: https://stackoverflow.com/questions/36499362/save-default-address-programatically-in-magento2

** Magento product image zoom demo: http://magento2.softdy.com/hero-hoodie.html

** Limit SEARCH autocomplete results:
	tores > Settings > Configuration > Catalog > Catalog > Catalog Search > Autocomplete Suggestions Count (and adjust value).

** Magento2 Custom Action Logging: http://inchoo.net/magento/logging-user-customer-actions-in-magento/

** Enable Magento Exception log:
	https://magento.stackexchange.com/questions/94530/how-to-enable-error-and-exception-logging-in-magento2
	
** Run composer changes (eg: install a module/library via composer - put json inside composer.json):
	composer update
	......................................
	composer update
	bin/magento setup:upgrade
	bin/magento setup:di:compile
	......................................

* Turn on display_errors on CLI:
	php -d display_errors bin/magento >log.txt
	
** Very nice magento2 link to read (Magento command line customization - prepare a new cli command, Magento Folder Structure):
	https://inviqa.com/blog/magento-2-tutorial-how-to-create-command-line-module



Login customer using USERNAME/email: https://github.com/diglin/Diglin_Username2 
------------------------------------------

TROUBLESHOOTINGS (Self):

Pages were showing 404 error on Staging (UAT) - (Refer ticket https://support.magento.com/hc/en-us/requests/89056) 
Solution by Magento Support:
We found that the cause of the issue in flag table
9 | staging                          |     0 | a:1:{s:15:"current_version";s:10:"1517922000";} | 2018-02-06 13:23:54
We updated it to "NULL" value and now site worked as expected
 DateTimeZone::__construct(): Unknown or bad timezone ()
	- catalogsearch_fulltext 
		Catalog Search indexer process unknown error: 
		Warning: Invalid argument supplied for foreach() in /app/7redg7uykvdko_stg/vendor/magento/module-media-storage/Model/File/Validator/NotProtectedExtension.php on line 86 
	Solution for above 2:
		DELETE FROM core_config_data WHERE path LIKE 'general' AND value IS NULL LIMIT 1;
		Ref: https://magento.stackexchange.com/questions/135188/my-magento-2-website-is-crashed-unknown-or-bad-timezone-error
			 https://stackoverflow.com/questions/26255953/php-foreach-error-while-uploading-product-image-in-magento
			 
Magento2 Re-indexing issues:
		https://github.com/magento/magento2/issues/10531
				........................
				Enable maintenance mode: bin/magento maintenance:enable
				Reset indexes: bin/magento indexer:reset
				
				Make sure that no database processes regarding indexing is running
				Open your database administration client like PHPmyadmin
				Run query: SHOW PROCESSLIST;
				Run query: KILL QUERY xxxxx (where xxxxx is the ID of processes you want to kill)
				
				bin/magento setup:upgrade
				bin/magento cache:clean
				bin/magento setup:static-content:deploy -j 1
				bin/magento indexer:reindex
				
				Disable maintenance mode: bin/magento maintenance:disable
				
				Now the only thin missing is some of the product images on the category page. The weird thing is that if i go to the product page I can see the product image. There are also a small version in the cache folder
				........................
				
When CSS/JS not loading, try this (did not work):
		Stores>Configuration>Advanced>Developer>Sign Static Files(Yes->No)
		Or, Insert core_config_data (config_id, scope, scope_id, path, value) values (null, 'default', 0, 'dev/static/sign', 0);
		Or, update core_config_data set value=0 where path like 'dev/static/sign';
------------------------------------------
	
Apply debug backtrace in magento:
$debugBackTrace = debug_backtrace(DEBUG_BACKTRACE_IGNORE_ARGS); foreach ($debugBackTrace as $item) { echo @$item['class'] . @$item['type'] . @$item['function'] . "\n"; }


Git remove untracked files:
    git clean -fd [To remove directories, run git clean -f -d or git clean -fd]
  git clean -fX [To remove ignored files, run git clean -f -X or git clean -fX]
https://stackoverflow.com/questions/61212/how-to-remove-local-untracked-files-from-the-current-git-working-tree 

* Exclude files/folder from merge:
	git reset HEAD -- app/code/Address
	git checkout -- app/code/Address
	
** GIT issue bad index:
	rm .git/index
	git reset

** 10k Limitation on Magento Search Results:
http://www.credevator.com/magento2-how-to-override-the-product-list-limit-on-category-page-in-magento-2/
https://bugs.koha-community.org/bugzilla3/show_bug.cgi?id=19502  [Debajyoti]

** STORE CREDIT in Magento:
https://bsscommerce.com/blog/how-set-up-use-magento-2-enterprise-store-credit-functionality/ 
http://www.saviost.net/magento-2-add-update-store-credit-customer-balance-by-custom-script/ 
http://socialhook.me/sh/programming/questions/17040183/how+do+i+update+customer+store+credit+programmatically 

** Paid Extension for One Step Checkout:
https://www.mageplaza.com/magento-2-one-step-checkout-extension/ 
	http://osc.demo.mageplaza.com/onestepcheckout/ [Frontend Demo page]

** Promo Code Paid Extension (suggested by Debajyoti on 10 May 2018):
    Please check the attached file for Promotion rules. Following is the best coupon module for Magento 2, however, before purchase, we need to communicate with Amasty for our different requirements.
URL: https://amasty.com/multiple-coupons-for-magento-2.html 

** Promo Code: Export promo code and start/expiry date of coupan code, one paid extension is available (19 Jul 2018):
https://amasty.com/generate-and-import-coupons-for-magento-2.html 
Or check this> https://github.com/landofcoder/MAGENTO-2-COUPON-EXTENSION 

** Bundle Product Promo Code Rule - cart price rule for Bundle Product:
https://www.mexbs.com/bundled-discount-magento2-extension 

** Product with Custom Options (Manage Absolute price):
https://bsscommerce.com/magento-2-custom-option-extensions/magento-2-custom-option-absolute-price-and-quantity-extension.html 

** Magento2 Product Import:
	[Paid extension - Purchased by Sajid]
	https://www.commerceextensions.com/magento-product-import-export.html
https://www.commerceextensions.com/magento-product-import-export-magento-2.html [Magento 2]
	http://docs.magento.com/m2/ce/user_guide/system/data-import.html
	
https://github.com/firebearstudio/importexportfree	[Free basic extension]
https://firebearstudio.com/the-improved-import.html [ 3000 products / min ]
	
	
	[Check Below for Magento2 Custom Import]
	https://www.alexcorradi.org/blog/a-guide-on-how-to-import-export-products-in-magento-2  [Very Nice Link to understand magento product import, Check its custom module]
	https://magento.stackexchange.com/questions/169419/how-to-create-a-custom-import-in-magento-2

** Search result page: vendor/magento/module-catalog-search/view/frontend/templates/advanced/result.phtml

** Wrap CMS page with additional HTML (via layout update xml):
	https://mage2.pro/t/topic/753

** Get parent product for Group/Bundle product in magento:
	https://www.mageplaza.com/get-parent-product-bundle-grouped-products-in-magento-2.html

** Magento 2 Autocomplete search: https://github.com/Sebwite/Magento2-SmartSearch

** Magento 2.3 Free extension for CMS advanced features: https://www.bluefootcms.com/ (check Demo)
	Extension Download: https://github.com/fisheyehq/module-bluefoot-list
	https://magento.stackexchange.com/questions/167570/bluefoot-cms-for-magento-2 [ extension not available ]

	https://github.com/genecommerce/Blue-Foot-Documentation/blob/master/README.md
	
	https://magento.com/blog/magento-news/magento-acquires-technology-behind-bluefoot-cms-page-builder
	https://www.bluefootcms.com/user-guides/pagebuilder/content-types
	
	[Coming in 2018 with Magento EE 2.3]
	https://pbs.twimg.com/media/DDQHrtjXkAIjzFg.jpg  [Announcement]
	https://www.williamscommerce.com/blog/popular-bluefoot-cms-page-builder-module-fully-integrated-magento-2-3/

* Verify XSD File: http://visualxsd.com/  (or, xmlspy)
	
* Google Analytics:
	https://www.fastcomet.com/tutorials/magento2/google-analytics
	
	Events:
		 onClick="ga('send','event','Link','Click','Contact Us');"
		 
	
* Magento Breadcrumb Issue: 
				https://gist.github.com/mbahar/82703c4b95d924d9bc8e6990202fdeba
				https://github.com/magento/magento2/issues/7967
				
* Restore the MySql DB (suggested by Cloud Support):
	gzip -d /app/7redg7uykvdko_stg/var/db_dump_qa2_07nov17.sql.gz	[Uncompress zip sql file]
	mysql -uUSER -p DATABASE_NAME < /path/to/backup.sql

* [PHP/.htaccess] Open .ics file in Outlook (Add to Calender):
		AddType text/calendar .ics  [keep it in .htaccess]
		https://stackoverflow.com/questions/5329529/i-want-html-link-to-ics-file-to-open-in-calendar-app-when-clicked-currently-op
	

* Magento CLI Commands Overview:
	https://www.magestore.com/magento-2-tutorial/use-commands-magento-2-cli-part-9/
	https://www.magestore.com/magento-2-tutorial/use-commands-magento-2-cli-part-10/
	
* Create Simple Products Programatically: https://magento.stackexchange.com/questions/102922/programmatically-create-a-simple-product-in-magento-2
		
* Import products programatically:
	https://www.pearlbells.co.uk/import-magento-2-products-programmatically/
	https://magento.stackexchange.com/questions/102922/programmatically-create-a-simple-product-in-magento-2
	
* Read/Write CSV File in Magento: https://www.magestore.com/magento-2-tutorial/how-to-readwrite-csv-file-from-magento/
	
* Unlock Admin User (cli command): php bin/magento admin:user:unlock ADMINUSERNAME
* Create Admin User (CLI): php bin/magento admin:user:create --admin-user="admin" --admin-password="admin@123" --admin-email="tanseera@chetu.com" --admin-firstname="Mayank" --admin-lastname="Kumar"
* Admin Password expiry: Stores > Configuration > Advanced > Admin > Security and set value for Password Lifetime (days) .

* Run test script file from Magento2: https://magento.stackexchange.com/questions/39981/how-can-i-bootstrap-magento-2-in-a-test-php-script

* PHPExcel Library: https://github.com/PHPOffice/PHPExcel/tree/1.8/Classes/PHPExcel
			https://magento.stackexchange.com/questions/100766/how-to-include-3rd-party-library-in-magento-2-like-php-xlsx-library

* IFrame Responsiveness:
	https://benmarshall.me/responsive-iframes/

* Mini Basket Session refresh issue: https://magento.stackexchange.com/questions/100615/magento-2-how-can-refresh-minicart-cache-after-clear-cart-session-and-place-orde

* Google Analytics Integration:
	https://www.customerparadigm.com/how-to-integrate-google-analytics-with-magento-2/
	Free extension (community): https://github.com/mageplaza/magento-2-google-analytics

* Unable to retrieve deployment version of static files from the file system (Strange Error when running setup:upgrade after module installation)
	Ref: https://magento.stackexchange.com/questions/178565/strange-error-when-running-setupupgrade-after-module-installation
		UPDATE core_config_data SET value = 0 WHERE path = 'dev/static/sign'
		Or, If record not exist then run below query to Insert record, run below query:
		INSERT INTO core_config_data VALUES (null, 'default' , 0, 'dev/static/sign', 0);
	
* Magento Order REST API:
		https://github.com/acolono/php-magento-api-sandbox/blob/master/api.php
	
Create REST Based APIs in Magento2:
	https://webkul.com/blog/magento2-custom-rest-api/ 
-------------------
PHP hints:
-------------------
php --ini   [command to check php.ini path i.e. php configuration file]

------------------------------------------------------------------------------------------------------
Upgrade Magento 2.1 to 2.2:
https://devdocs.magento.com/guides/v2.2/cloud/project/project-upgrade.html 

------------------------------------ Checkout Hints --------------------------------------------

Checkout Customisation Dev docs Link:
https://devdocs.magento.com/guides/v2.0/howdoi/checkout/checkout_new_field.html 
To show CART items on right sidebar on checkout:
Admin -> Configuration -> sales -> Accordian Checkout (earlier Cleancheckout):
Always Show Cart Items -> YES
Config files for checkout:
/var/www/dev/extensions/Bsigroup/AccordionCheckout/src/ConfigProvider/CheckoutConfigProvider.php
/var/www/dev/extensions/Bsigroup/AccordionCheckout/src/Model/ExtendedCheckoutConfigProvider.php

→ Add Billing Address step on Checkout:
    https://webkul.com/blog/add-billing-address-step-checkout-magento-2/ 

Additional Ecom API on checkout load:
[Called ecom api on checkout load in below file]
/var/www/staging_local/extensions/Bsigroup/AccordionCheckout/src/view/frontend/web/js/view/welcome.js


Checkout Related ADMIN changes:
	Sales -> Checkout Suite -> Extended Checkout Settings
	

‘Complete Order’ button does not work: https://standardsstoreproject.atlassian.net/browse/SS-687 
Hint: This error occurs as ‘Region’ is optional and value not entered for address  
Go to: Admin -> General -> State Options:



→ Postcode validation (by Sajid):
/var/www/dev/extensions/Bsigroup/AccordionCheckout/src/view/frontend/web/js/view/billing-address.js  -> postcodeValidation..

→ Add sap_order_id in sales_order table:
	/var/www/dev/extensions/Bsigroup/AccordionCheckout/src/Setup/UpgradeData.php
	-> installSalesData()

Reformatting Shipping Address for custom_attributes:
/var/www/dev/extensions/Bsigroup/AccordionCheckout/src/view/frontend/web/js/action/create-shipping-address-mixin.js
/var/www/dev/extensions/Bsigroup/AccordionCheckout/src/view/frontend/web/js/checkout-data.js 
To modify Address form fields:
/var/www/dev/extensions/Bsigroup/AccordionCheckout/src/Plugin/ModifyCheckoutLayoutPlugin.php
To add additional product meta data values in $item in checkout:
/var/www/dev/extensions/Bsigroup/AccordionCheckout/src/Plugin/Magento/Quote/Model/Item/ConfigProviderPlugin.php

To disable the Member Credit (Pay by Invoice) payment method when Membership Product is included in Basket:
/var/www/dev/extensions/Bsigroup/MemberCredit/view/frontend/web/js/view/payment/membercredit_gateway.js 


To override DISCOUNT block in Order Summary (right side bar:
https://magento.stackexchange.com/questions/190688/cart-price-rule-discount-description-does-not-displayed-on-cart-page-in-magento 
Template ref: /var/www/dev/vendor/magento/module-sales-rule/view/frontend/web/template/summary/discount.html 
***************************************************************************
Ecom API: Credit Exposure API Hints (Files info):

modified:   extensions/Bsigroup/AccordionCheckout/src/view/frontend/web/js/view/ecom-api/ecom-request.js
	modified:   extensions/Bsigroup/EcomApi/Helper/Curl.php
	modified:   extensions/Bsigroup/EcomApi/Model/Connector/Ecom/Request.php
	modified:   extensions/Bsigroup/EcomApi/etc/adminhtml/system.xml
	modified:   extensions/Bsigroup/EcomApi/etc/config.xml
	modified:   extensions/Bsigroup/MemberCredit/view/frontend/web/js/view/payment/method-renderer/membercredit_gateway.js
	modified:   extensions/Bsigroup/OrderExport/Api/VerifyRepositoryInterface.php
	modified:   extensions/Bsigroup/OrderExport/Model/VerifyRepository.php
	modified:   extensions/Bsigroup/OrderExport/etc/webapi.xml

1) To remove condition for using default DWH credit amount when Ecom API fails (ask Richa):
[Line #56]....if (!isNaN(ecom_creditexposure_response)) /var/www/dev/extensions/Bsigroup/MemberCredit/view/frontend/web/js/view/payment/method-renderer/membercredit_gateway.js

To remove the extra block showing Credit Applied (Better to Set Magento’s Store Credit instead of below - stored in ‘magento_customerbalance’ table):
/var/www/dev/extensions/Bsigroup/AccordionCheckout/src/view/frontend/web/js/view/payment/customer-balance.js
Commented Template as below:
//template: 'Bsigroup_AccordionCheckout/payment/customer-balance'
***************************************************************************


Ecom API Payload setting Hints:
	/var/www/dev/extensions/Bsigroup/EcomApi/Model/Connector/Ecom/Request.php -> execute()
	/var/www/dev/extensions/Bsigroup/EcomApi/Model/Connector/Ecom/Export.php

‘OrderCreate’ Ecom API Call - to create order in SAP after Magento place order:
	/var/www/dev/extensions/Bsigroup/OrderExport/Model/Data/Order.php
‘OrderVerify’ Ecom API Call - to update VAT & Price from SAP on Magento Review Order:
	/var/www/dev/extensions/Bsigroup/OrderExport/Model/Data/Quote.php

Constant defined for Allowed Product Types (Standards: 6, Books: 3) to be included in Ecom API:
/var/www/dev/extensions/Bsigroup/EcomApi/Helper/Data.php -> getAllowedSAPProdTypes()
To make changes in Checkout Sidebar and Review Order (Pranabesh made changes for Event detail):
	 .../Bsi/Shop/Magento_Sales/templates/order/info.phtml
 .../view/frontend/web/js/view/summary/item/details.js
 .../frontend/web/template/summary/item/details.html



Checkout To Check (self):
Move billing address form to shipping address:
https://magento.stackexchange.com/questions/189853/move-billing-address-form-to-shipping-address-page-in-magento-2-1/205532?utm_medium=organic&utm_source=google_rich_qa&utm_campaign=google_rich_qa

To fetch curl timeout value from config and use it in below:
/var/www/dev/extensions/Bsigroup/EcomApi/Helper/Curl.php   → exec()

Move Billing Address under Shipping Address:
https://github.com/sohelrana09/modified-checkout

Add custom Field inside Shipping Address Form:
https://www.edmondscommerce.co.uk/handbook/Platforms/Magento-2/Custom-Shipping-Address-Field/
https://devdocs.magento.com/guides/v2.2/howdoi/checkout/checkout_new_field.html 

Customise one page checkout in Magento2:
https://www.magestore.com/magento-2-tutorial/magento-2-checkout-customization/ 
Move Billing Address to Shipping Address:
https://ranasohel.me/2017/12/17/move-billing-address-under-shipping-address-in-magento-2-checkout/ 
Free module for above: https://github.com/sohelrana09/modified-checkout 
Customise Shipping Address on Checkout:
https://magento.stackexchange.com/questions/202724/save-custom-field-in-shipping-address-at-checkout-in-magento-2?utm_medium=organic&utm_source=google_rich_qa&utm_campaign=google_rich_qa 
Carrier with such method not found: %1, %2 (when saving New Billing Address for PDF download and click Enter Payment Details - done by overriding ShippingInformationManagent)
https://github.com/magento/magento2/issues/13594 

======================================================================

Get Promo Code Rule detail from Quote/Order:
https://magento.stackexchange.com/questions/160000/how-to-load-a-discount-rule-by-id-in-magento-2 [Quote]


======================================================================


Issues in Magento:
"Save to Address Book" in Admin checkout causes duplicate address book entries:
https://github.com/magento/magento2/issues/8181




INGENICO HINTS:
CFT-2018-504906:
The feedback parameter NCERRORPLUS is available (and configured on your test account BSIStandard) as part of the direct link post-sale response. This parameter should give a description of the error that is returned. It is not however available as a feedback parameter for standard eCommerce.

------------------------------------------------------- JAVASCRIPT ---------------------------------------
Remove specific items from Array using jQuery:
var y = [1, 2, 2, 3, 2] var removeItem = 2; y = jQuery.grep(y, function(value) { return value != removeItem; });


---------------------- HINTS FROM OUR TEAM DEVELOPMENT -----------------------
- Customer Service Log module (Sanjib):
	app/code/Log/Menu
	
- Customer Service - Notes module (Sanjib):
	app/code/Notes/CustomerEdit
	
- Customer bought also bought:
	app/code/Vovayatsyuk/Alsoviewed
		
- Postcode lookup extension:
	app/code/Craftyclicks/Ukpostcodelookup
https://github.com/craftyclicks/magento2-ukpostcodelookup 

- Membership Form:
https://standards-storeqa.bsigroup.com//Memberdata/index/Membershipproducttwo
app/code/Member/Data [Module Path]
------------------------------------------------------------------------------
Magento2 Free Extensions:

https://github.com/mageplaza/magento-2-security 

https://github.com/prince108/magento2-extrafee [Adding extra tax]

https://github.com/bangerkuwranger/Magento-2-GTID-Safe-URL-Rewrite-Tables  [https://github.com/magento/magento2/issues/12124]

Magento2 Free extension for One page Checkout:
install this free module via composer: https://github.com/danslo/CleanCheckout
They just need to run below command:
composer require rubic/magento2-module-clean-checkout
Or, https://github.com/danslo/CleanCheckoutCore
Demo Url: https://demo.cleancheckout.com/
Another Free plugn (but not better than above): https://www.iwdagency.com/extensions/one-step-page-checkout.html


--------------------------------------------------------------------
GDPR free extension:
https://github.com/mageplaza/magento-2-gdpr
Or, download from : https://www.mageplaza.com/magento-2-gdpr-extension/
https://www.mageplaza.com/kb/gdpr-delete-customer-account.html 
composer require mageplaza/module-gdpr
php bin/magento setup:upgrade
php bin/magento setup:static-content:deploy
.................................................................................
Issues for applying CART RULE on customer group:

https://github.com/magento/magento2/issues/10009
https://github.com/magento/magento2/issues/10103
.................................................................................
Advanced CMS extension: https://www.advancedcontentmanager.com/demo/

ACM2 Support: https://help.bird.eu/servicedesk/customer/portal/6/HELP-964
	https://www.advancedcontentmanager.com/documentation/m2/developers/overriding-templates 
.................................................................................
Upload Image in Magento 2: https://webkul.com/blog/how-to-upload-image-in-magento2/

Add New Field in Checkout: http://devdocs.magento.com/guides/v2.0/howdoi/checkout/checkout_new_field.html
Add New Form in Checkout: http://devdocs.magento.com/guides/v2.0/howdoi/checkout/checkout_form.html

.................................................................................
Add Custom Field in CMS: https://www.magevision.com/blog/post/add-custom-field-to-cms-page-magento-2/
                         https://github.com/magevision/blog/tree/master/AddCustomFieldtoCMSPage/app/code/MageVision/Blog15
.................................................................................
VERY NICE GITHUB REPO FOR MAGENTO 2 EXTENSIONS & HINTS:
https://github.com/magento/magento2/tree/develop/app/code/Magento
.................................................................................


SELF HINTS


---------------------- Magento Upgrade TO DO (Highlights) -------------------------
Date: 25 Oct 2018
Major activities to be performed during magento upgrade are below. Actually it could be easy if magento standards are followed in all levels of customisation (e.g. No custom queries, Proper use of Magento functions, Use of Composer, No changes done in Core modules including Paid/Free Extensions):
​Send all existing working patches of magento 2.1.8 ver. to the Support Team for review and confirmation

Contact Paid/Free extension support teams to provide compatible extension ver. for magento 2.2.x
Webkul (Search Layered Navigation)
Amasty (Advanced Catalog Permissions)
Ingenico (ePayments)
RedChamp (Meta Robots)
PluginCompany (CMS Version Control)
CraftyClicks (UK PostCode LookUp)
Product ImportExport


Identify all changes done within Contributed/Paid extensions (E.g.: Product ImportExport, Ingenico, Webkul, CraftyClicks)
[This was not recommended still I see changes are done within extension files - So we need keep those changes with the new version of extension]


Try to upgrade via Composer - for this all our extensions need to have composer.json file


Check the release note of magento ver. 2.2.x and identify all functions/constructs changed from 2.1.8 to 2.2.x - We need to replace them into all our customizations ==> Needed for both Custom Modules as well Themes


Identity all magento configuration changes between 2.1.8 to 2.2.x and maintain version changes


Configuration changes in Contributed/Paid extensions due to their version upgrade (if any) - Need to check compatibility


[Steps to be performed in upgrade as we can not do it via Composer in our case]
​Take any development branch (e.g. DEV, QA2, QA4, QA5)


Upgrade basic magento version -> Raise a ticket to magento if required to have a vanilla Magento 2.2.x version


Use of latest compatible Build hooks for magento 2.2.x (changes to be done in .magento.app.yaml - refer magento documentation) 


Keep BSI Theme & all custom/contributed/paid modules (Latest ver.) into their respective folders


Run composer update


Run Compilation commands (e..g Cache Clean, Setup Upgrade, Compile)


Update setup version & schema version in setup_module table if 


Review logs and admin configuration are properly in place and correct as per magento 2.2.x


Thoroughly test after all changes done --> ALL SET


.................................................................................

.................................................................................

.................................................................................

25
- Course: Leading SAFe v1    5940
- Exam: SAFe Agilist v1 - 5007
- Functional TAG Interviewing Skills Enhancement Program WBT - 52732
- Process Intellectual Property Rights - An Introduction_WBT  v1 53993   
- Process DEG-ECoE Estimation Concepts Training TCS_elementary_WBT v1 - 5474
- Behavioral Mentoring Workshop_ILT/VILT v1 - 53080
- PMs Confluence - ILT v1 - 45788
- Eminence Technology Talk Show v1 - 49420
- CLI - Language Tips for Everyday Business - WBT v1 - 42580
- CLI - Language Tips for Virtual Conferencing - WBT v1 - 49805
- CLI - English Grammar Nuggets Comparing and Evaluating_WBT v1 - 51657
- CLI - English Grammar Nuggets Articles - WBT v1 - 49961
- CLI - English Grammar Nuggets Dependent Prepositions - WBT v1 - 49863
- RiO - Softskill for Application Operations_Team members_Workshop_VILT v1   51422
- SkillSoft - Generating Creative and Innovative Ideas - WBT v1 - 24689
- BPS - Business Innovation_Lynda v1 - 54262
- Foundation : Unix/Linux basics and commands_Awareness_iONLX_SP_Assessment v1 51176
- Process - Intellectual Property Rights - An Introduction_WBT v1 - 53993
- PHP Basic training - webex
- MySql training - webex
- PHP Advanced training - webex
- Magento training - webex
---------------------------
25
Course: Leading SAFe v1    5940
Exam: SAFe Agilist v1 - 5007
TAG Interviewing Skills Enhancement Program WBT - 52732
IPR - An Introduction_WBT  v1 53993   
DEG-ECoE Estimation Concepts v1 - 5474
Behavioral Mentoring Workshop_ILT VILT v1 - 53080
PMs Confluence - ILT v1-45788
Eminence Technology Talk Show v1 - 49420
Language Tips for Everyday Business - WBT v1 - 42580
Language Tips for Virtual Conferencing - WBT v1 - 49805
English Grammar Nuggets Comparing and Evaluating_WBT v1 - 51657
English Grammar Nuggets Articles - WBT v1 - 49961
English Grammar Nuggets Dependent Prepositions - WBT v1 - 49863
Softskill for Application Operations_Team members_Workshop_VILT v1   51422
Generating Creative and Innovative Ideas - WBT v1 - 24689
BPS-54262
Foundation : Unix/Linux basics and commands_Awareness_iONLX_SP_Assessment v1 51176
PHP Basic training - webex
MySql training - webex
PHP Advanced training - webex
Magento training - webex
