# api-gateaway-with-ocelot
A gateaway api implemented with Ocelot library.

# Getting started
Run all api.
Using Postman, send request to http://localhost:7000/bar.(You can find all definitions of services in ocelot.json)

You can find ocelot.json below :

{
  "Routes": [
    {
      "DownstreamPathTemplate": "/api/product",
      "DownstreamScheme": "http",
      "DownstreamHostAndPorts": [
        {
          "Host": "localhost",
          "Port": 7002
        }
      ],
      "UpstreamPathTemplate": "/bar",
      "UpstreamHttpMethod": [ "Get" ]
    },
    {
      "DownstreamPathTemplate": "/api/customer/foo",
      "DownstreamScheme": "http",
      "DownstreamHostAndPorts": [
        {
          "Host": "localhost",
          "Port": 7001
        }
      ],
      "UpstreamPathTemplate": "/foo",
      "UpstreamHttpMethod": [ "Get" ],
      "RateLimitOptions": {
        "ClientWhitelist": [],
        "EnableRateLimiting": true,
        "Period": "1m",
        "PeriodTimespan": 60,
        "Limit": 10
      }
    }
  ],
  "GlobalConfiguration": {
    "BaseUrl": "https://localhost:7000"
  }
}
