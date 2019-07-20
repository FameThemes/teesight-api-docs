```php

$url = 'https://teesight.me/wp-json/ts/v1/order';
$token =  'a1befc42-d425-46fe-a001-d255553f2d31';
$data = array(
	'test_token' => 'a1befc42-d425-46fe-a001-d255553f2d31',
	'password' => '1234xyz',
	'my_content' => 'Sa Hoang',
);


$ch = curl_init();
curl_setopt( $ch, CURLOPT_URL, $url );
curl_setopt( $ch, CURLOPT_CUSTOMREQUEST, 'POST');
curl_setopt( $ch, CURLOPT_POSTFIELDS, json_encode( $data ) );  // Post Fields
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
