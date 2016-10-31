# aliyun-php-sdk-sms
阿里云短信服务提供composer解决方案
# install
$ composer require luyisuifeng/aliyun-php-sdk-sms
#demo
use Aliyun\Core\Profile\DefaultProfile;  
use Aliyun\Core\DefaultAcsClient;  
use Aliyun\Core\Exception\ClientException;  
use Aliyun\Core\Exception\ServerException;  
use Aliyun\Core\Regions\Endpoint;  
use Aliyun\Core\Regions\EndpointProvider;  
use Aliyun\Core\Regions\EndpointConfig;  
use Aliyun\Core\Sms\Request\V20160927\SingleSendSmsRequest;  
$iClientProfile = DefaultProfile::getProfile('cn-hangzhou', 'your accessKeyId', 'your accessSecret);  
$client = new DefaultAcsClient($iClientProfile);  
$config = new EndpointConfig();  
$endpoint = new Endpoint('cn-hangzhou', $config->getRegionIds(), $config->getProductDomains());  
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
