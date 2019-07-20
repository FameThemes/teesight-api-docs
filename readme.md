## Create new order

```php

$url = 'https://teesight.me/wp-json/ts/v1/order';
$token =  'a1befc42-d425-46fe-a001-d255553f2d31';
$order_data = array();


$ch = curl_init();
curl_setopt( $ch, CURLOPT_URL, $url );
curl_setopt( $ch, CURLOPT_CUSTOMREQUEST, 'POST');
curl_setopt( $ch, CURLOPT_POSTFIELDS, json_encode( $order_data ) );  // Post Fields
curl_setopt( $ch, CURLOPT_RETURNTRANSFER, true );
curl_setopt( $ch, CURLOPT_SSL_VERIFYPEER, false );

$headers = [
	'Content-Type: application/json; charset=utf-8',
	'access-token: '.$token,
];
curl_setopt( $ch, CURLOPT_HTTPHEADER, $headers );
$server_output = curl_exec( $ch );
curl_close( $ch );

var_dump( json_decode(  $server_output, true ) );
    
```

Example order data here https://github.com/shrimp2t/teesight-api-docs/blob/master/example-order.json
