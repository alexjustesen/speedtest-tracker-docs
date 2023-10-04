# Data Dictionary

### Tables

#### Results

<table><thead><tr><th width="181.66666666666666">Field</th><th width="188">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>id</code></td><td>primary key</td><td></td></tr><tr><td><code>ping</code></td><td>double</td><td>As milliseconds</td></tr><tr><td><code>download</code></td><td>unsigned big integer</td><td>As bytes</td></tr><tr><td><code>upload</code></td><td>unsigned big integer</td><td>As bytes</td></tr><tr><td><code>server_id</code></td><td>integer</td><td>ID of the speedtest server</td></tr><tr><td><code>server_host</code></td><td>string</td><td>Host/URL of the speedtest server</td></tr><tr><td><code>server_name</code></td><td>string</td><td>Name of the speedtest server</td></tr><tr><td><code>url</code></td><td>string</td><td>URL to the result on speedtest.net</td></tr><tr><td><code>comments</code></td><td>text</td><td>User added comments</td></tr><tr><td><code>scheduled</code></td><td>boolean</td><td>Was the result scheduled?</td></tr><tr><td><code>successful</code></td><td>boolean</td><td>Was the result successful?</td></tr><tr><td><code>data</code></td><td>json</td><td>The raw data received from the Speedtest CLI</td></tr><tr><td><code>created_at</code></td><td>timestamp</td><td></td></tr></tbody></table>
