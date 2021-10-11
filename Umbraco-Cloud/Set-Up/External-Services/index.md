---
versionFrom: 7.0.0
keywords: whitelist allow list allowlist ip internal
---

# Using external services with Umbraco Cloud

In some cases Umbraco Cloud might not be the only service you are working with. You might need to work with other services as well - this could be either internal or third party services. In either case, it will be services external to Umbraco Cloud.

When you are working with an external service that is behind a firewall and that service needs to communicate with your Umbraco Cloud project, you need to make sure the Umbraco Cloud Server IPs are allowed to bypass the firewall.

An example could be, that you're fetching some information from an external service which is behind a firewall. In order to give your Umbraco Cloud project access to the external service you need to add the IPs used by the Umbraco Cloud servers to an allow list (other services may refer to it as a "whitelist").

These are the IPs you will need to add:

```
52.166.147.129
13.95.93.29
40.68.36.142
13.94.247.45
52.157.96.229
```
:::note
Above IPs only apply to websites created before H1 2021 or websites that haven't been migrated to the new platform.
:::

As part of the [migration to our new platform](https://umbraco.com/blog/the-future-of-umbraco-cloud/) the outgoing IPs of the new platform are changing. Please reach out to support in order to get the outgoing IPs for your project.
These are the **out-going** IPs on the Umbraco Cloud servers. Whenever we add new IPs they will be updated here.

:::note
When new IPs are added we will also send the information directly to the [Technical Contacts](../Team-Members/Technical-Contact.md) for each Umbraco Cloud project.
:::

If you are using an external service that is not behind a firewall, you do not need to include the Umbraco Cloud IPs in an allow list.
