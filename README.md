Telegram Notify
================
Want to get notified once your code (that needs long execution time) has completed? With the use of IFTTT, you can send a POST request to a webhook and a notification will be sent to your Telegram Account

Set Up
--
* You will need an IFTTT account ([create here](https://ifttt.com/discover))
* Create a new Applet
* For "this", select Maker and select "Receive a web request"
* Under "Event Name", enter a name for your webhook (you will need this later to put inside your code).
* For "that", select Telegram and connect to your Telegram account (It will be easier if you have Telegram installed on your desktop)
* Once connected, choose the action "Send Message"
* For the "target chat" selection: you can choose to send via a private message or send to a group/channel
* For the "Message text" textfield, you can leave it as it is.
* Click "Create Action" and then "Finish" to complete.

Calling the Webhook
--
To call the webhook from your code, you will need to retrieve the Maker api key from your Maker's settings  ([go here](https://ifttt.com/services/maker/settings)). The API key is the last segment of the URL under the "Account Info"

Information on how to call the Maker API: https://maker.ifttt.com/use/REPLACE_ME_WITH_YOUR_API_KEY

You can now call your webhook from your code by making a POST request.

PHP Example:
```PHP
<?php
function sendTelegramNotification ($message) {
	$data = array("value1" => $message);
	$data_string = json_encode($data);
	$ch = curl_init('http://maker.ifttt.com/trigger/REPLACE_ME_WITH_YOUR_WEBHOOK_NAME/with/key/REPLACE_ME_WITH_YOUR_API_KEY');
	curl_setopt($ch, CURLOPT_CUSTOMREQUEST, "POST");
	curl_setopt($ch, CURLOPT_POSTFIELDS, $data_string);
	curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
	curl_setopt($ch, CURLOPT_HTTPHEADER, array(
	    'Content-Type: application/json',
	    'Content-Length: ' . strlen($data_string))
	);
	$result = curl_exec($ch);
}
?>
```
Example Usage
```PHP
sendTelegramNotification ("Your Message Here");
```
