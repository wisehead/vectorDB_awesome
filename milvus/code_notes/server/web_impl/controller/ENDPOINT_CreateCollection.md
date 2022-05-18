#1.ENDPOINT_CreateCollection

```
ENDPOINT("POST", "/collections", CreateCollection, BODY_DTO(CollectionRequestDto::ObjectWrapper, body))
--WebRequestHandler handler = WebRequestHandler();
--auto status_dto = handler.CreateCollection(body);
----WebRequestHandler::CreateCollection
```