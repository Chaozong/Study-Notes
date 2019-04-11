# SpringBoot常用类及其用法
## 使用RestTemplate
>org.springframework.web.client.RestTemplate

spring框架提供的RestTemplate类可用于在应用中调用rest服务，它简化了与http服务的通信方式，统一了RESTful的标准，封装了http链接， 我们只需要传入url及返回值类型即可(类似以前使用apache HttpClient之类的工具)。

### 用法
+ GET请求
```
// 1-getForObject()
User user1 = this.restTemplate.getForObject(uri, User.class);

// 2-getForEntity()
ResponseEntity<User> responseEntity1 = this.restTemplate.getForEntity(uri, User.class);
HttpStatus statusCode = responseEntity1.getStatusCode();
HttpHeaders header = responseEntity1.getHeaders();
User user2 = responseEntity1.getBody();
  
// 3-exchange()
RequestEntity requestEntity = RequestEntity.get(new URI(uri)).build();
ResponseEntity<User> responseEntity2 = this.restTemplate.exchange(requestEntity, User.class);
User user3 = responseEntity2.getBody();
```
+ 发送POST请求
```
// 1-postForObject()
User user1 = this.restTemplate.postForObject(uri, user, User.class);

// 2-postForEntity()
ResponseEntity<User> responseEntity1 = this.restTemplate.postForEntity(uri, user, User.class);

// 3-exchange()
RequestEntity<User> requestEntity = RequestEntity.post(new URI(uri)).body(user);
ResponseEntity<User> responseEntity2 = this.restTemplate.exchange(requestEntity, User.class);
```

+ 设置HTTP Header
```
// 1-Content-Type
RequestEntity<User> requestEntity = RequestEntity
        .post(new URI(uri))
        .contentType(MediaType.APPLICATION_JSON)
        .body(user);

// 2-Accept
RequestEntity<User> requestEntity = RequestEntity
        .post(new URI(uri))
        .accept(MediaType.APPLICATION_JSON)
        .body(user);

// 3-Other
RequestEntity<User> requestEntity = RequestEntity
        .post(new URI(uri))
        .header("Authorization", "Basic " + base64Credentials)
        .body(user);
```

+ 补获异常
```
try {
    responseEntity = restTemplate.exchange(requestEntity, String.class);
} catch (HttpServerErrorException e) {
    // log error
}
```

+ 下载文件
```
/ 小文件
RequestEntity requestEntity = RequestEntity.get(uri).build();
ResponseEntity<byte[]> responseEntity = restTemplate.exchange(requestEntity, byte[].class);
byte[] downloadContent = responseEntity.getBody();
  
// 大文件  
ResponseExtractor<ResponseEntity<File>> responseExtractor = new ResponseExtractor<ResponseEntity<File>>() {
    @Override
    public ResponseEntity<File> extractData(ClientHttpResponse response) throws IOException {
        File rcvFile = File.createTempFile("rcvFile", "zip");
        FileCopyUtils.copy(response.getBody(), new FileOutputStream(rcvFile));
        return ResponseEntity.status(response.getStatusCode()).headers(response.getHeaders()).body(rcvFile);
    }
};
File getFile = this.restTemplate.execute(targetUri, HttpMethod.GET, null, responseExtractor);
```
