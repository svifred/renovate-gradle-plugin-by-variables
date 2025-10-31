# 38984

[Renovate minimal reproduction](https://github.com/renovatebot/renovate/blob/main/docs/development/minimal-reproductions.md)
for discussion [#38984](https://github.com/renovatebot/renovate/discussions/38984).

## Current behavior

Renovate handles variables defined in `gradle.properties` differently
depending on whether they are used in `build.gradle.kts` or `settings.gradle.kts`.

In `build.gradle.kts`, variables:

* `quarkusPlatformGroupId` identifying group,
* `quarkusPlatformArtifactId` identifying artifact,
* `quarkusPlatformVersion` identifying version

are all expanded by Renovate, leading Renovate to correctly identify dependency and updates.

Conversely in `settings.gradle.kts`, variables:

* `quarkusPluginVersion` identifying the plugin version _is_ expanded,
* `quarkusPluginId` identifying plugin artifact is _NOT_ expanded.
 
effectively "hiding" the plugin from Renovate.

That `quarkusPluginVersion` is expanded can be seen by hardcoding the plugin id in `settings.gradle.kts` as follows:

```kotlin
id("io.quarkus") version quarkusPluginVersion
```

## Expected behavior

When given as in this reproduction, Renovate ought to expand variables identifying plugin and artifact alike.
I.e. when defined in `gradle.properties`, variables should be expanded in both `build.gradle.kts` and `settings.gradle.kts`.

## Link to the Renovate issue or Discussion

[#38984 Gradle: Variable for plugin id not expanded in settings.gradle.kts](https://github.com/renovatebot/renovate/discussions/38984).
