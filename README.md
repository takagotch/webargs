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
  
@use_args(hello_args)
async def echo_use_args(request, args):
  return json_response(args)

@use_kwargs(hello_args)
async def echo_use_kwargs(request, name):
  return json_response({"name": name})

@use_args({"value": fields.Int()}, validate=lambda args: args["value"] > 42)
async def echo_use_args_validated(request, args):
  return json_response(args)
  
async def echo_multi(request):
  parsed = await parser.parser(hello_multiple, request)
  return json_response(parsed)

async def echo_shema(request):
  parsed = await parser.parse(hello_many, request, locations=("json"),)
  return json_response(parsed)

@use_args({"value": fields.Int()})
async def echo_use_args_with_path_params(request, args):
  return json_response(args)

@use_kwargs({"value": fields.Int()})
async def echo_use_kwargs_with_path_params(request, value):
  return json_response({"value": value})
  
@use_args({"page": fields.Int(), "q": fields.Int()}, locations=("query"),)
@use_args({"name": fields.Str()}, locations=("json"),)
async def echo_use_args_multiple(request, query_parsed, json_parsed):
  return json_response({"query_parsed": query_parsed, "json_parsed": json_parsed})

async def always_error(request):
  def always_fail(value):
    raise ma.ValidationError("something went wrong")
    
  args = {"text": fields.Str(validate=always_fail)}
  parsed = await parser.parse(args, request)
  return json_response(parsed)

async def echo_headers(request):
  parsed = await parser.parse(hello_args, request, locations=("headers",))
  return json_response(parsed)


class EchoHandler:
  @use_args(hello_args)
  async def get(self, request, args):
    return json_response(args)
    
class EchoHandlerView(web.View):
  @asyncio.coroutine
  @use_args(hello_args)
  def get(self, args):
    return json_response(args)
    
@asyncio.corotine
@use_args(HelloSchema, as_kwargs=True)
def echo_use_schema_as_kwargs(requst, name):
  return json_response({"name": name})

def add_route(app, methods, route, handler):
  for method in methods:
    app.router.add_route(method, route, handler)
    
def create_app():
  app = aiohttp.web.Application()
  
  add_route(app, ["GET", "POST"], "/echo", echo)
  return app
```

```
```

```
```

