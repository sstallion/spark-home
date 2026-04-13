# Configuration

Spark Home relies on a single [yaml](http://yaml.org/) configuration file, located in the `/assets` directory.

> [!NOTE]  
> This fork is scoped to the DGX Spark home page. Most configuration options are pre-defined in the built-in defaults and do **not** need to be specified. Only the `services` list needs to be defined by the user. For the full list of configuration options, see the [Homer documentation](https://github.com/bastienwirtz/homer/blob/main/docs/configuration.md).

## User Configuration

The only value that must be defined by the user is the `services` list. The following example can be copied into `/assets/config.yml` as a starting point:

```yaml
---
# Homepage configuration

# Services
# First level array represents a group.
# Leave only an "items" key if not using group (group name, icon & tagstyle are optional, section separation will not be displayed).
services:
  - name: "My Applications"
    icon: "fas fa-code-branch"
    items:
      - name: "My App"
        logo: "assets/tools/sample.png"
        subtitle: "My application"
        tag: "app"
        url: "http://localhost:8080"
        target: "_blank"
```

View **[smart cards](customservices.md)** for details about available service card types and how to configure them.

`null` value or missing keys will be ignored and value from the `config.yml` will be used if available.
Empty values (either in `config.yml` or the endpoint data) will hide the element (ex: set `"title": ""` to hide the title bar).

## Default Configuration

The following values are set by default and do not need to be specified unless you wish to override them:

```yaml
---
title: Home
subtitle: DGX Spark
documentTitle: DGX Spark
logo: logo.png

header: true
footer: >
  <p>Made with <a href="https://github.com/bastienwirtz/homer/">Homer</a>.
  DGX, DGX SPARK, and the NVIDIA logo are trademarks and/or registered
  trademarks of NVIDIA Corporation in the U.S. and other countries.</p>

columns: 3
connectivityCheck: true

defaults:
  layout: list
  colorTheme: auto

theme: nvidia
colors: ~

message: ~

links:
  - name: Playbooks
    icon: fas fa-bookmark
    url: https://build.nvidia.com/spark
    target: _blank
  - name: User Guide
    icon: fas fa-book
    url: https://docs.nvidia.com/dgx/dgx-spark/
    target: _blank
  - name: Forum
    icon: fas fa-comments
    url: https://forums.developer.nvidia.com/c/accelerated-computing/dgx-spark-gb10
    target: _blank
  - name: FAQ
    icon: fas fa-circle-question
    url: https://forums.developer.nvidia.com/t/dgx-spark-gb10-faq/347344
    target: _blank
  - name: Support
    icon: fas fa-headset
    url: https://www.nvidia.com/en-us/support/dgx-spark/
    target: _blank

proxy: ~
```

## Connectivity checks

As a webapp (PWA) the dashboard can still be displayed when your homer server is offline.
The connectivity checker periodically sends a HEAD request bypassing the PWA cache to the dashbord page to make sure it's still reachable.

It can be useful when you access your dashboard through a VPN or ssh tunnel for example, to know if your conection is up. It also helps when using an authentication proxy, it will reload the page if the authentication expires (when a redirect is send in response to the HEAD request).
