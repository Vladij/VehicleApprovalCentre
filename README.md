# VehicleApprovalCentre
Documentation for integration CRM &amp;&amp; email sending 

The whole project is done according to Wordpress architecture. Link for documentation: https://codex.wordpress.org/

To use custom field output, we used the 'ACF' plugin. Link for documentation: https://www.advancedcustomfields.com/ 

To send email from the feedback form, we used the 'Contact Form 7 plugin'. Link for documentation: https://contactform7.com/
Fields :
	Your name 	  : [text-839],
	Your phone 	  : [text-840],
	Email address : [email-123]

Integration to CRM. Link: https://leads.vehicleapprovalcentre.ca/

Executable file: site_dir/wp-content/themes/marshal/functions.php

Display function: 'kviz_1()'

Input data:
	Method : POST
	Action :
		wp_ajax_kviz 		: for authorized user
		wp_ajax_nopriv_kviz : for not authorized/quest user
Link to documentation: https://developer.wordpress.org/plugins/javascript/ajax/

Variables 
	$url - url to send post messages to CRM (https://leads.vehicleapprovalcentre.ca/tradingapi/api/DirectPost/PostRequest)
	$data - returned array with form
		fields from $data :
			'MinimumBidPrice' => 0.00 									(integer, default 0.00)
			'LeadTypeId' => 6 											(integer, default 6)
			'IsTest' => false 											(bool, true/false)
			'FirstName' => $_POST['CRM']['FirstName'] 					(string, data from form)
			'LastName' => $_POST['CRM']['LastName'] 					(string, data from form)
			'AddressLine1' => $_POST['CRM']['AddressLine1'] 			(string, data from form)
			'PostalCode' => $_POST['CRM']['PostalCode'] 				(string, data from form)
			'City' => $_POST['CRM']['City'] 							(string, data from form)
			'Province' => $_POST['CRM']['Province'] 					(string, data from form)
			'HomePhone' => $_POST['CRM']['HomePhone'] 					(string, data from form)
			'Email' => $_POST['CRM']['Email'] 							(string, data from form)
			'Country' => "Canada" 										(string, defaut value 'Canada')
			'EmployerMonths' => $_POST['CRM']['EmployerMonths'] 		(integer, data from form)
			'Income' => $_POST['CRM']['Income'] 						(integer, data from form)
			'JobTitle' => $_POST['CRM']['JobTitle'] 					(string, data from form)
			'ResidenceCost' => $_POST['CRM']['ResidenceCost'] 			(float, data from form)
			'ResidenceYears' => $_POST['CRM']['ResidenceYears'] 		(integer, data from form)
			'EmployerName' => $_POST['CRM']['EmployerName'] 			(string, data from form)
			'ResidenceType' => $_POST['CRM']['ResidenceType'] 			(string, data from form)
			'EmploymentStatus' => $_POST['CRM']['EmploymentStatus'] 	(string, data from form)
			'EmployerYears' => $_POST['CRM']['EmployerYears'] 			(string, data from form)
			'VehicleType' => $_POST['CRM']['VehicleType'] 				(string, data from form)
			'VehicleBudget' => $_POST['CRM']['VehicleBudget'] 			(string, data from form)
			'PassCode' => '*******-****-****-****-**********' 			(string, your passcode for connect to CRM)
			'DOB' => $_POST['CRM']['DOB'] 								(string, data from form)
			'TradeIn' => $_POST['CRM']['TradeIn'] 						(string, data from form)

	$options - array options to send post. Link to documentation: https://www.w3schools.com/php/func_network_header.asp
	$context - creates and returns a stream context with any options supplied in options preset. Options ($options) must be an associative array of associative arrays in 			   the format $arr['wrapper']['option'] = $value. It defaults to an empty array.
	$result - file_get_contents(), see documentation php: https://www.php.net/manual/en/function.file-get-contents.php
	wp_die() - indicate the function that the processing is completed