{{site.data.alerts.callout_info}}
Because core changefeeds return results differently than other SQL statements, they require a dedicated database connection with specific settings around result buffering. In normal operation, CockroachDB improves performance by buffering results server-side before returning them to a client. This can cause unbounded delivery latency for core changefeeds, so the `results_buffer_size` connection string parameter is used to disable buffering. Core changefeeds also have different cancellation behavior than other queries: they can only be canceled by closing the underlying connection or issuing a  [`CANCEL QUERY`](cancel-query.html) statement on a separate connection. Combined, these attributes of changefeeds mean that applications should explicitly create dedicated connections to consume changefeed data, instead of using a connection pool as most client drivers do by default.
{{site.data.alerts.end}}