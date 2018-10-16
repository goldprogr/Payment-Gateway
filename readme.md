


How It Works
----------------

**A. Website Owner / Seller Side**

You can use the following steps to sell your products on your website for cryptocoins if you wish to and can automatically convert them to USD

* [Install](https://gourl.io/api-php.html#installation) GoUrl crypto Payment Box on your website and dynamically configure order id, currency, amount to pay, etc. Or use [Monetiser Online](https://gourl.io/view/newurl/Cryptocoin_Monetiser_Make_Money_Online.html) if you don't have your own website.
* You can accept payments in Bitcoins only or you can accept other coins - Bitcoin Cash, Dogecoin, Litecoin, Dash, etc also. See [Demo1](https://gourl.io/lib/examples/pay-per-product-multi.php) (multiple coins) or [Demo2](https://gourl.io/lib/examples/pay-per-membership.php?gourlcryptocoin=bitcoin) (Bitcoin only)
* When you [setup](https://gourl.io/editrecord/coin_boxes/0) Cryptocoin Payment Box, you can enter the [original amount](https://gourl.io/images/instruction-config2.png) in USD or in cryptocoins. The USD amount will be automatically converted to cryptocoin amount using today's LIVE cryptocurrency exchange rates (updated every 30 minutes) and the cryptocoin amount will be displayed in the payment box. For example, if you entered 20 USD, it will display 0.059 BTC in the payment box.
* You will need to create an account on [Poloniex.com](https://poloniex.com/) or on [Bitstamp.net](https://www.bitstamp.net/) (trading platforms)
* [Setup](https://gourl.io/images/instruction-config3.png) so that all your received payments are automatically forwarded from your GoUrl.io account to your account on Poloniex / Bitstamp (enter your Poloniex/Bitstamp coin wallet address in gourl [payment box settings](https://gourl.io/images/instruction-config3.png)). And use the "autosell" feature (auto trade your cryptocoins to USD) on Poloniex/Bitstamp.
* Using that functionality you don't need to worry if cryptocurrency prices go down or up. Within 1-2 hours after a cryptocoin payment has been received by you, your payment will be automatically converted to USD on Poloniex/Bitstamp and will be kept on your Poloniex/Bitstamp USD account.
* Later you can withdraw your USD from Poloniex/Bitstamp to your own USA/UK/France/etc bank account


**B. End User / Buyer Side**

* All your users will see GoUrl [Payment Box](https://gourl.io/api-php.html#live) on your webpage, and some users will use their coin wallets and make payments to you
* In around 5 seconds after cryptocoin payment is made, user will see confirmation on your website page that payment is received (i.e. very fast)
* Your website will automatically immediately receive current user id with full payment information from our payment server
* The user will still be on your webpage and see that successful payment result, your script can automatically process payment and give user confirmation (for example, upgrading user membership or giving download link on your products, etc). All in automatic mode - no manual actions are needed
* For user that payment procedure on your website will be looking very similar visually and compare with normal credit cards for its speed
* No paperwork, no chargebacks, no monthly fee, low transaction fee ([from 0%](https://gourl.io/#section4)). Please note that during the next 30 minutes (after transaction is verified) payment will be automatically forwarded to your wallet address



Installation - PHP Script
----------------------------
* [Free Register](https://gourl.io/view/registration/New_User_Registration.html) or [Login](https://gourl.io/info/memberarea/My_Account.html) on the website and [create new payment box](https://gourl.io/editrecord/coin_boxes/0)
* [Download](https://coins.gourl.io/lib/cryptoapi_php.rar) Free PHP/MySQL Script and read [How It Works](https://gourl.io/#section8)
* Edit file [cryptobox_config.php](https://github.com/cryptoapi/Payment-Gateway/blob/master/lib/cryptobox.config.php), add your db details and your private key ([screenshot](https://gourl.io/images/instruction-config1.png))
* Run [SQL query](https://github.com/cryptoapi/Payment-Gateway#mysql-table) in your database to create new table crypto_payments
* Place your public/private keys from new created payment box in any [example](https://github.com/cryptoapi/Payment-Gateway/tree/master/Examples)
* You can use this [example](https://github.com/cryptoapi/Payment-Gateway/blob/master/Examples/pay-per-product.php) ([screenshot](https://gourl.io/images/instruction-config2.png)) and run it

THAT'S IT! CRYPTOCOIN PAYMENT BOX/CAPTCHA SHOULD NOW BE WORKING ON YOUR SITE.

Read more - [https://gourl.io/api-php.html](https://gourl.io/api-php.html)



Installation - Wordpress Plugin
----------------------------




MySQL Table
-----------------

Please also run MySQL query below which will create MySQL
table where all the cryptocoin payments made to you will 
be stored.
You can have multiple crypto boxes on site, all of them
relates to your different crypto boxes and will be stored
in that one table :


	CREATE TABLE `crypto_payments` (
	  `paymentID` int(11) unsigned NOT NULL AUTO_INCREMENT,
	  `boxID` int(11) unsigned NOT NULL DEFAULT '0',
	  `boxType` enum('paymentbox','captchabox') NOT NULL,
	  `orderID` varchar(50) NOT NULL DEFAULT '',
	  `userID` varchar(50) NOT NULL DEFAULT '',
	  `countryID` varchar(3) NOT NULL DEFAULT '',
	  `coinLabel` varchar(6) NOT NULL DEFAULT '',
	  `amount` double(20,8) NOT NULL DEFAULT '0.00000000',
	  `amountUSD` double(20,8) NOT NULL DEFAULT '0.00000000',
	  `unrecognised` tinyint(1) unsigned NOT NULL DEFAULT '0',
	  `addr` varchar(34) NOT NULL DEFAULT '',
	  `txID` char(64) NOT NULL DEFAULT '',
	  `txDate` datetime DEFAULT NULL,
	  `txConfirmed` tinyint(1) unsigned NOT NULL DEFAULT '0',
	  `txCheckDate` datetime DEFAULT NULL,
	  `processed` tinyint(1) unsigned NOT NULL DEFAULT '0',
	  `processedDate` datetime DEFAULT NULL,
	  `recordCreated` datetime DEFAULT NULL,
	  PRIMARY KEY (`paymentID`),
	  KEY `boxID` (`boxID`),
	  KEY `boxType` (`boxType`),
	  KEY `userID` (`userID`),
	  KEY `countryID` (`countryID`),
	  KEY `orderID` (`orderID`),
	  KEY `amount` (`amount`),
	  KEY `amountUSD` (`amountUSD`),
	  KEY `coinLabel` (`coinLabel`),
	  KEY `unrecognised` (`unrecognised`),
	  KEY `addr` (`addr`),
	  KEY `txID` (`txID`),
	  KEY `txDate` (`txDate`),
	  KEY `txConfirmed` (`txConfirmed`),
	  KEY `txCheckDate` (`txCheckDate`),
	  KEY `processed` (`processed`),
	  KEY `processedDate` (`processedDate`),
	  KEY `recordCreated` (`recordCreated`),
	  KEY `key1` (`boxID`,`orderID`),
	  KEY `key2` (`boxID`,`orderID`,`userID`),
	  UNIQUE KEY `key3` (`boxID`, `orderID`, `userID`, `txID`, `amount`, `addr`)
	) ENGINE=InnoDB DEFAULT CHARSET=utf8 ROW_FORMAT=DYNAMIC;


.

	
Payment API List :
---------------------

* [Bitcoin Payment API](https://gourl.io/bitcoin-payment-gateway-api.html)
* [Bitcoin Cash Payment API](https://gourl.io/bitcoincash-payment-gateway-api.html)
* [Litecoin Payment API](https://gourl.io/litecoin-payment-gateway-api.html)
* [Dash Payment API](https://gourl.io/dash-payment-gateway-api.html)
* [Dogecoin Payment API](https://gourl.io/dogecoin-payment-gateway-api.html)
* [Speedcoin Payment API](https://gourl.io/speedcoin-payment-gateway-api.html)
* [Reddcoin Payment API](https://gourl.io/reddcoin-payment-gateway-api.html)
* [Potcoin Payment API](https://gourl.io/potcoin-payment-gateway-api.html)
* [Feathercoin Payment API](https://gourl.io/feathercoin-payment-gateway-api.html)
* [Vertcoin Payment API](https://gourl.io/vertcoin-payment-gateway-api.html)
* [UniversalCurrency Payment API](https://gourl.io/universalcurrency-payment-gateway-api.html)
* [MonetaryUnit Payment API](https://gourl.io/monetaryunit-payment-gateway-api.html)
* [Peercoin Payment API](https://gourl.io/peercoin-payment-gateway-api.html)


.


PHP Examples / Live Demo :
-----------------------------

* **White Label Product**  Bitcoin Payments - [your logo/jquery](https://gourl.io/lib/examples/example_customize_box.php)
* **Pay-Per-Product**: Example1 - [multiple crypto](https://gourl.io/lib/examples/pay-per-product-multi.php), Example2 - [bitcoin](https://gourl.io/lib/examples/pay-per-product.php)
* **Pay-Per-Download**: Example3 - [multiple crypto](https://gourl.io/lib/examples/pay-per-download-multi.php), Example4 - [bitcoin](https://gourl.io/lib/examples/pay-per-download.php)
* **Pay-Per-Post**: Example5 - [multiple crypto](https://gourl.io/lib/examples/pay-per-post-multi.php), Example6 - [bitcoin](https://gourl.io/lib/examples/pay-per-post.php)
* **Pay-Per-Registration**: Example7 - [multiple crypto](https://gourl.io/lib/examples/pay-per-registration-multi.php), Example8 - [bitcoin](https://gourl.io/lib/examples/pay-per-registration.php)
* **Pay-Per-Page-Access**: Example19 - [multiple crypto](https://gourl.io/lib/examples/pay-per-page-multi.php), Example10 - [bitcoin](https://gourl.io/lib/examples/pay-per-page.php)
* **Pay-Per-Membership**: Example11 - [multiple crypto](https://gourl.io/lib/examples/pay-per-membership-multi.php), Example12 - [bitcoin](https://gourl.io/lib/examples/pay-per-membership.php) 
