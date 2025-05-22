# Authorization

A "Bearer Token" is required to authenticate into the API, you can generate tokens for your user account on `/admin/api-tokens`.&#x20;

### Token Abilities

Each token is provisioned with one or more abilities. When calling an endpoint, the token must include the ability required by that endpoint

| Abilities     | Description                     |
| ------------- | ------------------------------- |
| Read Results  | Allows token to read results.   |
| Run Speedtest | Allows token to run speedtests. |
| List servers  | Allows token to list servers.   |

