# OpenSearch Dashboards

You can access OpenSearch Dashboards at [http://localhost:5601](http://localhost:5601).
Dashboard can be configured with a default index pattern `fess.*` to view the indexed data.
It also has an index for the Fess logs `fess_log.*` which can be used to monitor different aspects of the Fess server.
There is also an index for the Fess configuration `fess_config.*` which can be used to monitor the configuration changes.
This is the actual location where the Fess configuration is stored. Fess uses OpenSearch's bulk API to import and export configuration.

Included by Fess there is a default configuration to set up Dashboards for monitoring the Fess server.
This can be imported from the `fess_log.ndjson` file in the `dashboards` directory.
See the [README](../compose/dashboards/extension/kibana//README.md) for more information.
