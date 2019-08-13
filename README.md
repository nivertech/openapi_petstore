# OpenAPIPetstore

This is a sample server Petstore server. For this sample, you can use the api key &#x60;special-key&#x60; to test the authorization filters.

### Building

To install the required dependencies and to build the elixir project, run:
```
mix local.hex --force
mix do deps.get, compile
```

## Installation

If [available in Hex](https://hex.pm/docs/publish), the package can be installed
by adding `open_api_petstore` to your list of dependencies in `mix.exs`:

```elixir
def deps do
  [{:open_api_petstore, "~> 0.1.0"}]
end
```

Documentation can be generated with [ExDoc](https://github.com/elixir-lang/ex_doc)
and published on [HexDocs](https://hexdocs.pm). Once published, the docs can
be found at [https://hexdocs.pm/open_api_petstore](https://hexdocs.pm/open_api_petstore).

# How to generate Elixir code

``` bash
# install the OpenAPI CLI generator
npm install @openapitools/openapi-generator-cli -g

# Download the PetStore API definition
wget https://raw.githubusercontent.com/openapitools/openapi-generator/master/modules/openapi-generator/src/test/resources/2_0/petstore.yaml

mkdir -p openapi_petstore

# generate elixir code
openapi-generator generate -i petstore.yaml -g elixir -o openapi_petstore/

cd openapi_petstore/

mix deps.get

mix compile

iex -S mix
```

# How to run

``` elixir
alias OpenAPIPetstore.Connection
alias OpenAPIPetstore.Api.Store

token = "special-key"

iex(8)> conn = Connection.new(token)
%Tesla.Client{
  adapter: nil,
  fun: nil,
  post: [],
  pre: [
    {Tesla.Middleware.Headers, :call,
     [[{"authorization", "Bearer special-key"}]]}
  ]
}

iex(12)> {ok, inventory} = Store.get_inventory(conn)
{:ok,
 %{
   "1234567891234" => 1,
   "767778" => 1,
   "AVAILABLE" => 14,
   "Nonavailable" => 1,
   "Not Found" => 1,
   "OFF" => 1,
   "ON" => 4,
   "PENDING" => 18,
   "Pending" => 2,
   "Ready" => 1,
   "Reserved" => 1,
   "SOLD" => 20,
   "amet" => 1,
   "available" => 1062,
   "available;pending;sold" => 4,
   "avaliable" => 1,
   "c" => 1,
   "def" => 1,
   "ksks" => 1,
   "pending" => 355,
   "snatched" => 2,
   "sold" => 358,
   "string" => 30,
   "swimming" => 1,
   "unavailable" => 2,
   "{{petStatus}}" => 1
 }}

```
