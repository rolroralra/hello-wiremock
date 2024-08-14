# WireMock 
[WireMock 공식 홈페이지](https://wiremock.org/)

## Just Try
```bash
docker-compose up -d
```

And then, access to `http://localhost:8080/__admin/mappings` in your browser.

```json
{
  "mappings": [
    {
      "id": "a37c5ea0-5874-47c6-a3be-33f60eb68ced",
      "request": {
        "url": "/api/v1/hello",
        "method": "GET"
      },
      "response": {
        "status": 200,
        "bodyFileName": "response.json",
        "headers": {
          "Content-Type": "application/json"
        }
      },
      "uuid": "a37c5ea0-5874-47c6-a3be-33f60eb68ced"
    }
  ],
  "meta": {
    "total": 1
  }
}
```

And verify the response by sending a request to `http://localhost:8080/api/v1/hello`.

```json
{
  "message": "Hello, WireMock from file!"
}
```

## Get Started (WireMock)
- [Get Started by JUnit5](https://wiremock.org/docs/junit-jupiter/)
- [Get Started by Docker](https://wiremock.org/docs/standalone/docker/)
- [Get Started by standalone](https://wiremock.org/docs/standalone/java-jar/)

## 기본 구조
```bash
./wiremock
├── __files
│   └── response.json
├── extensions
│   └── wiremock-webhooks-extension-3.9.1.jar
└── mappings
    └── mapping.json
```

## Stubbing & Verifying 
- [Stubbing](https://wiremock.org/docs/stubbing/)
- [Request Matching](https://wiremock.org/docs/request-matching/)
- [Response Templating](https://wiremock.org/docs/response-templating/)
- [Simulating Faults](https://wiremock.org/docs/simulating-faults/)
- [Proxying](https://wiremock.org/docs/proxying/)
- [Verifying](https://wiremock.org/docs/verifying/)

## Other Protocol
- [WebHook & Callback](https://wiremock.org/docs/webhooks-and-callbacks/)
- [Mocking GRPC](https://wiremock.org/docs/grpc/)
- [Mocking GraphQL](https://wiremock.org/docs/solutions/graphql/)
- [JWT](https://wiremock.org/docs/jwt/)
- [HTTPS](https://wiremock.org/docs/https/)

## Extending WireMock (Customizing)
- [WireMock Extensions](https://wiremock.org/docs/extending-wiremock/)