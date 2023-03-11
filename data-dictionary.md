# Data Dictionary

### Tables

#### Results

| Field         | Type                 | Description                                  |
| ------------- | -------------------- | -------------------------------------------- |
| `id`          | primary key          |                                              |
| `ping`        | double               | As milliseconds                              |
| `download`    | unsigned big integer | As bytes                                     |
| `upload`      | unsigned big integer | As bytes                                     |
| `server_id`   | integer              | ID of the speedtest server                   |
| `server_host` | string               | Host/URL of the speedtest server             |
| `server_name` | string               | Name of the speedtest server                 |
| `url`         | string               | URL to the result on speedtest.net           |
| `comments`    | text                 | User added comments                          |
| `scheduled`   | boolean              | Was the result scheduled?                    |
| `successful`  | boolean              | Was the result successful?                   |
| `data`        | json                 | The raw data received from the Speedtest CLI |
| `created_at`  | timestamp            |                                              |
