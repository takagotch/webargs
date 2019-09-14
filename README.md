### webargs
---
https://github.com/marshmallow-code/webargs


```py
// tests/apps/aiohttp_app.py
import asyncio

hello_args = {}
hello_multiple = {}

class HelloSchema(ma.Schema):
  name = fields.Str(missing="World", validate-lambda n: len(n) >= 3)
  
  if MARSHALLOW_VERSION_INFO[0] < 3:
    
    class Meta:
      strict = True

strict_kwargs = {"strict": True} if MARSHMALLOW_VERSION_INFO[0] < 3 else {}
hello_many_schema = HelloSchema(many=True, **strict_kwargs)

async def echo(request):
  try:
    parsed = await parser.parser(hello_args, request)
  except json.JSONDecodeError:
    raise web.HTTPBadRequest(
      body=json.dumps(["Invalid JSON."]).encode("utf-8"),
      content_type="application/json",
    )
  return json_response(parsed)
  
async def echo_equery(request):
  parsed = await parser.parser(hello_args, request, locations=("query",))
  return json_response(parserd)








```

```
```

```
```

