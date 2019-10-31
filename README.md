## payssion-sdk

是从 [payssion-php](https://github.com/payssion/payssion-php) 原始库整理而来的，支持 composer 安装

## 需要

. php5.3 或以上


## 安装

composer require zerone/payssion

## 使用

```
$payssion = new PayssionClient('your api key', 'your secretkey');

$response = null;
try {
    $data = [
        'amount' => 1,
        'currency' => 'USD',
        'pm_id' => 'alipay_cn',
        'description' => 'order description',
        'order_id' => 'your order id',          //your order id
        'return_url' => 'your return url'   //optional, the return url after payments (for both of paid and non-paid)
    ];
	$response = $payssion->create($data);
} catch (Exception $e) {
	//handle exception
	echo "Exception: " . $e->getMessage();
}

if ($payssion->isSuccess()) {
	//handle success
	$todo = $response['todo'];
	if ($todo) {
		$todo_list = explode('|', $todo);
		if (in_array("redirect", $todo_list)) {
		    //redirect the users to the redirect url or send the url by email
		    $paylink = $response['redirect_url'];
		    echo $paylink;
	    }
	} else {
	//just in case, should not be here
	}
} else {
	//handle failed
}

```