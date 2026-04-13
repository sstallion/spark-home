# Smart cards

Smart cards provide specific integrations for external services, displaying additional information and extra features beyond a basic service card. They are enabled by adding a `type` key to a service item in your YAML configuration.

> [!NOTE]  
> This fork is scoped to the DGX Spark home page and does **not** include the upstream service integrations.

If you need to add a custom service card, `Generic.vue` (`src/components/services/Generic.vue`) is still available as a base component. It provides three named slots — `icon`, `content`, and `indicator` — that you can extend.

For the full list of upstream service integrations and their configuration options, see the [Homer documentation](https://github.com/bastienwirtz/homer/blob/main/docs/customservices.md).
