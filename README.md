# aliyun-php-sdk-sms
阿里云短信服务提供composer解决方案
# install
$ composer require luyisuifeng/aliyun-php-sdk-sms
#demo
$iClientProfile = DefaultProfile::getProfile('cn-hangzhou', 'your accessKeyId', 'your accessSecret);
$client = new DefaultAcsClient($iClientProfile);
$config = new EndpointConfig();
$endpoint = new Endpoint(config::get('cn-hangzhou'), $config->getRegionIds(), $config->getProductDomains());
$endpoints = array( $endpoint );
EndpointProvider::setEndpoints($endpoints);
$request = new SingleSendSmsRequest();
$request->setSignName('XXXX');  //签名名称
$request->setTemplateCode('SMS_123456');  //模板id
$request->setRecNum('138xxx');//目标手机号
$request->setParamString("{\"goodname\":\"商品名\",\"specinfo\":\"商品属性\"}");//模板变量，数字一定要转换为字符串
try {
    $response = $client->getAcsResponse($request);
    print_r($response);
}
catch (ClientException  $e) {
    print_r($e->getErrorCode());
    print_r($e->getErrorMessage());
}
catch (ServerException  $e) {
    print_r($e->getErrorCode());
    print_r($e->getErrorMessage());
}
