# Data Dictionary

### Tables

#### Results

<table><thead><tr><th width="181.66666666666666">Field</th><th width="188">Type</th><th>Description</th></tr></thead><tbody><tr><td><code>id</code></td><td>primary key</td><td></td></tr><tr><td><code>service</code></td><td>string</td><td>Service user to run the speedtest.</td></tr><tr><td><code>ping</code></td><td>double</td><td>As milliseconds</td></tr><tr><td><code>download</code></td><td>unsigned big int</td><td>As bytes</td></tr><tr><td><code>upload</code></td><td>unsigned big int</td><td>As bytes</td></tr><tr><td><code>comments</code></td><td>text</td><td>User added comments.</td></tr><tr><td><code>data</code></td><td>json</td><td>The raw response from the speedtest.</td></tr><tr><td><code>status</code></td><td>string</td><td><ul><li><strong>Completed</strong> - a speedtest that ran successfully.</li><li><strong>Failed</strong> - a speedtest that failed to run successfully.</li><li><strong>Started</strong> - a speedtest that has been started but has not finished running.</li></ul></td></tr><tr><td><code>scheduled</code></td><td>boolean</td><td>Was the result scheduled.</td></tr><tr><td><code>created_at</code></td><td>timestamp</td><td>When the record was created.</td></tr><tr><td><code>updated_at</code></td><td>timestamp</td><td>When the record was last updated.</td></tr></tbody></table>
