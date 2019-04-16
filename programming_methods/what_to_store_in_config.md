# What to store in config file?

서비스를 개발하던 중에 현재 환율 정보를 가져와야 하는 api를 개발하게 되었다.
물론 금융 사이트 등에서 raw data를 가져오는 방법도 있지만, 이미 공개되어 있는 api를 끌어다 써보기로 했다.
Googling 결과 찾은 게 바로 [Currencylayer](https://currencylayer.com/)라는 친구였다.

일반적으로 API를 사용하기 위해서는 사용자에게 발급된 access key가 필요하다.
(Sign-up을 하면 access key를 발급해준다.)
이 key를 URL에 포함하여 request를 보내면 response를 받는 방식으로 동작한다.

그렇게 currencylayer를 활용해서 API 파일을 열심히 작성했는데 한 가지 실수한 점이 있었다.

``` php
// ExchangeRate.php
Class ExchangeRate
{
  private $access_key = 'feiun38h19e3c20181dewkd';
  private $url = 'http://apilayer.net/api';
  private $endpoint = 'live';

  public function _process(HttpRequest $req): void
  {
    // ...
  }
}
```

API 파일의 class property로 access key를 적었던 것이다.
이것이 문제가 되는 이유는, 가장 먼저 이 코드를 본 사람이 해당 key를 가지고 currencylayer에 pay하지 않고 그 api 서비스를 이용할 수 있게 된다는 점이다.
다음으로 API 파일의 목적은 http request를 받아 로직에 따라 response를 보내는 것인데(일종의 machine), 이런 access key와 같은 정보들은 redundant하다는 것이다.
따라서, access key와 같이 설정값들은 config 파일에 분리하여 보관하는 것이 좋다고 한다.
설정 값들이 live server, dev server 또 alpha-test, beta-test에서 각각 다른 값으로 사용할 수 있기 때문에 이렇게 관리하는 것에 이점이 있다.

``` php
// ExchageRateConfig.php
class ExchangeRateConfig
{
  private $access_key = 'dfeiun38h19e3c20181dewkd';
  private $base_url = 'http://apilayer.net/api/';
  private $endpoint = 'live';

  public static $instance;

  public static function getInstance(): self
  {
    if (empty(self::$instance)) {
      self::$instance = new self();
    }

    return self::$instance;
  }

  public function getAccessKey() {
    return $this->access_key;
  }

  public function getBaseURL() {
    return $this->base_url;
  }

  public function getEndpoint() {
    return $this->endpoint;
  }
}
```

``` php
// ExchangeRate.php
class ExchangeRate
{
  private $access_key;
  private $base_url;
  private $endpoint;

  public function _init(HttpRequest $request): void
  {
  $config = ExchangeRateConfig::getInstance();
  $this->access_key = $config->getAccessKey();
  $this->base_url = $config->getBaseURL();
  $this->endpoint = $config->getEndpoint();
  }

  public function _process(HttpRequest $req): void
  {
    // ...
  }
}
```
