# Changelog

## v0.11.0

* Added handling of rate limiting from the Rollbar API.

## v0.10.0

* **BREAKING CHANGE**: Increased Elixir version requirement to 1.4 and higher.
* Made invalid configurations raise.
* Allowed to configure Rollbax to use a proxy (#105).

## v0.9.2

* Fixed some code that wouldn't let Rollbax start if `:enabled` was `false` but the access token or environment were not set.

## v0.9.1

* Fixed a bug where we didn't list Jason as an application in the `:applications` key.

## v0.9.0

* **BREAKING CHANGE**: Increased Elixir version requirement to 1.3 and higher.
* Introduced `Rollbax.report_message/4`.
* Reworked logging support. Now `Rollbax.Logger` is not a `Logger` backend, and you cannot send logs to Rollbar automatically via `Logger.*` macros (Rollbar is not a logging aggregation service after all! :stuck_out_tongue:). Use `Rollbax.report_message/4` instead. Check out the documentation for more information on how to use the new `Rollbax.Logger`.
* Made the `:access_token` configuration parameter be only required if `:enabled` is `true`.
* Added support for customizing the Rollbar API endpoint.
* Stopped overriding occurrence data provided by the user.
* Added support for runtime configuration through a callback that can be set with `:config_callback`.
* Dropped support for configuring some options through `{:system, variable}` "special" values. The new `:config_callback` configuration option allows to fetch variables from the environment at runtime, so that should be used instead.

## v0.8.2

* Made sure that JSON encoding never cause `Rollbax.Client` crashing.
* Improved formatting of stacktraces, and exceptions reported as exits.
* Fixed a possible infinite loop when a report is send while `Rollbax.Client` is not available.

## v0.8.1

* Fixed a bug when reporting a term that is not an exception and using kind `:error` in `Rollbax.report/5`.

## v0.8.0

* Fixed a bug with custom data not being reported correctly.
* Bumped Elixir requirement from ~> 1.0 to ~> 1.1.

## v0.7.0

* Added support for blacklisting logger messages through the `:blacklist` configuration option. This way, it's possible to prevent logged messages that match a given pattern from being reported.
* Started allowing globally-set custom data: the data in the `:custom` configuration option for the `:rollbax` application is now sent alongside everything reported to Rollbax (and merged with report-specific custom data).

## v0.6.1

* Fixed a bug involving invalid unicode codepoints in `Rollbax.Logger`.

## v0.6.0

* Removed `Rollbax.report/2` in favour of `Rollbax.report/3`: this new function takes the "kind" of the exception (`:error`, `:exit`, or `:throw`) so that items on Rollbar are displayed more nicely.
* Renamed `Rollbax.Notifier` to `Rollbax.Logger`.
* Started logging (with level `:error`) when the Rollbar API replies with an error.
* Started putting the metadata associated with `Logger` calls in the `"message"` part of the reported item instead of the `"custom"` data associated with it.
