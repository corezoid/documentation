# Erlang

```Erlang
-module(test).

-export([send_to_conv/6, test/0]).

test() ->
%Conveyor url
  ConvUrl = "https://api.corezoid.com",

%Conveyor ID
  ConvId = <<"5555">>,

%API user login (Conveyor with given ConvId has to be shared for this API user)
  ApiUser = "555",

%API User Secret Key
  ApiSecret = <<"qjVXiaXFazSCtIvMTjW29cZbPkzeYUzCzGmmrcJtIIj2eqceUm">>,

  % unique task reference, optional
  Reference = integer_to_binary(random:uniform(100000000)),

% Data for processing
  Data = <<"{\"phone\":\"client_phone\",\"name\":\"client_name\"}">>,

  {ok, Response} = send_to_conv(ConvUrl, ConvId, ApiUser, ApiSecret, Reference, Data),

  Response.


-spec send_to_conv(ConvUrl, ConvId, ApiUser, ApiSecret, Reference, Data) -> {ok, binary()} when
  ConvUrl :: list(),
  ConvId :: binary(),
  ApiUser :: list(),
  ApiSecret :: binary(),
  Reference :: binary(),
  Data :: binary().

send_to_conv(ConvUrl, ConvId, ApiUser, ApiSecret, Reference, Data) ->

% start inets app for httpc client
  application:start(inets),

%Time in unix format
  Time = erlang:integer_to_binary(unixtime()),

%Request with one element (could be many) in ops array for task create
  Request = <<"{\"ops\":[{\"ref\":\"", Reference/binary, "\",\"type\":\"create\",\"obj\":\"task\",\"conv_id\":\"",
  ConvId/binary, "\",\"data\":", Data/binary, "}]}">>,

%Generate Sign
  Sign = create_sign(<<Time/binary, ApiSecret/binary, Request/binary, ApiSecret/binary>>),
  Url = ConvUrl ++ "/api/1/json/" ++ ApiUser ++ "/" ++ binary_to_list(Time) ++ "/" ++ binary_to_list(Sign),

  {ok, {{_, 200, _}, _, Response}} = httpc:request(post, {Url, [], "application/octet-stream", Request}, [{timeout, 10000}], []),

  {ok, Response}.


unixtime()->
  {A,B,_C} = now(),
  A*1000000 + B.

create_sign(Bin) ->
  list_to_binary(list_to_hexstr(binary_to_list(crypto:hash(sha, Bin)))).


list_to_hexstr([]) ->
  [];
list_to_hexstr([H|T]) ->
  to_hex(H) ++ list_to_hexstr(T).


to_hex(N) when N < 256 ->
  [hex(N div 16), hex(N rem 16)].


hex(V) ->
  if
    V < 10 ->
      $0 + V;
    true ->
      $a + (V - 10)
  end.
```
