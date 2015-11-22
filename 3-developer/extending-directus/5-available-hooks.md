# Hooks

Hooks allow project-specific (non-Directus core) code to interact directly with Directus core events. The two hooks which are currently supported are `postUpdate` and `postInsert`, which enable logic to react to Directus record update and insert events, respectively. The hooks are very simple to implement: just add custom logic to the (untracked) config file at  /directus/api/configuration.php. [See this example configuration file as a reference.](https://github.com/RNGR/directus6/blob/f386da45a4957f776c4a701fdd31aae2c93e1273/api/configuration.example.php#L31)
