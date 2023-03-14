# Request Payload 처리
```python
class Item(BaseModel):
    name: str
    description: str | None = None
    price: float
    tax: float | None = None

@app.post("/items")
async def create_item(item: Item):
    return item
```

만약 ``name``, ``price`` 데이터를 보내지 않는다면 오류가 뜨지만, ``description``, ``tax``는 필수 값이 아니다.

아래와 같이 경로, 쿼리 파라미터와 같이 쓸 수 있다.
```python
class Item(BaseModel):
    name: str
    description: str | None = None
    price: float
    tax: float | None = None

@app.put("/items/{item_id}")
async def create_item(item_id: int, item: Item, q: str | None = None):
    result = {"item_id": item_id, **item.dict()}
    if q:
        result.update({"q": q})
    return result
```
