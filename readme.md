## API end point
LIVE: https://seller.teesight.com/wp-json/ts/v1/order

TEST: https://server.teesight.com/wp-json/ts/v1/order

## Submit new order

```php

$url = 'https://server.teesight.com/wp-json/ts/v1/order';
$token =  'a1befc42-d425-46fe-a001-d255553f2d31';
$order_data = array();


$ch = curl_init();
curl_setopt( $ch, CURLOPT_URL, $url );
curl_setopt( $ch, CURLOPT_CUSTOMREQUEST, 'POST');
curl_setopt( $ch, CURLOPT_POSTFIELDS, json_encode( $order_data ) );
curl_setopt( $ch, CURLOPT_RETURNTRANSFER, true );
curl_setopt( $ch, CURLOPT_SSL_VERIFYPEER, false );

$headers = [
	'Content-Type: application/json; charset=utf-8',
	'access-token: '.$token,
];
curl_setopt( $ch, CURLOPT_HTTPHEADER, $headers );
$server_output = curl_exec( $ch );
curl_close( $ch );

// Dump respond
var_dump( json_decode(  $server_output, true ) );
    
```

Example order data here https://github.com/FameThemes/teesight-api-docs/blob/master/example-order.json


## Example response data success

```json
{
	"code" : "success",
	"status" : 200,
}
```


## Example response data error
```json
{
	"code" : "error",
	"error_code" : "error_code",
	"message" : "Error message",
	"status" : 200,
}
```

## Example webhook reciever
When order item tracking code is changed, we will send a webhook to your site.
First, go to Orders -> Webhook URL to add your Webhook, see: https://cl.ly/a4be150abe2e 
To receive the data, you can follow this code:
```php
if ( isset( $_SERVER['HTTP_X_TS_WEBHOOK_SOURCE'] ) && false !== strpos( $_SERVER['HTTP_X_TS_WEBHOOK_SOURCE'], 'teesight' ) ) {
	$input = @file_get_contents( 'php://input' );
	$data = wp_parse_args(
		json_decode( $input, true ), 
		array(
			'order_id'      => '',
			'line_item_id'  => '',
			'tracking_code' => '',
			'sent_from'     => '',
			'action'        => '',
		) 
	);

	if ( $data['order_id'] && $data['tracking_code'] ) {
		// Do your stuff.
	}
}
```


