

## 配置文件

```
public class RestTemplateConfig {
    @Bean
    public RestTemplate restTemplate(ClientHttpRequestFactory factory) {
        return new RestTemplate(factory);
    }

    @Bean
    public ClientHttpRequestFactory simpleClientHttpRequestFactory() {
        SimpleClientHttpRequestFactory factory = new SimpleClientHttpRequestFactory();
        //超时设置
        factory.setReadTimeout(30000);//ms
        factory.setConnectTimeout(30000);//ms
        return factory;
    }
}
```



## Post请求



### json格式

```
RestTemplate restTemplate = new RestTemplate();

//设置请求头
HttpHeaders headers = new HttpHeaders();
headers.setContentType(MediaType.APPLICATION_JSON);
headers.set("token","your Token" );

//设置请求体
String jsonBody = "{\"key1\":\"value1\",\"key2\":\"value2\"}";
HttpEntity<String> requestEntity = new HttpEntity<>(jsonBody, headers);

String url = "http://example.com/api/endpoint";

//发送请求，并获取返回信息
ResponseEntity<String> responseEntity = restTemplate.exchange(url, HttpMethod.POST, requestEntity, String.class);

int statusCode = responseEntity.getStatusCodeValue();
HttpHeaders responseHeaders = responseEntity.getHeaders();
String responseBody = responseEntity.getBody();
```

