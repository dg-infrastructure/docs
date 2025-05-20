# Feature Flags

Pipelines supports optional feature flags that allow you to enable or disable specific behaviors. You can configure these flags by setting them as environment variables within your [HCL](/2.0/reference/pipelines/configurations-as-code/api#env-block) or [YAML](/2.0/reference/pipelines/configurations#env) configuration files.


## Available Flags

#### `PIPELINES_FEATURE_EXPERIMENT_ALL`
<ul>
<li>
Enables all experiment flags.
</li>
<li>
**Default Value**: Disabled
</li>
<li>
**How to Enable**: Set to `"true"`
</li>
</ul>

#### `PIPELINES_FEATURE_EXPERIMENT_AGGRESSIVE_CONSOLIDATION`
<ul>
<li>
Enables Pipelines to consolidate as many Terragrunt plan/apply changes as possible into a single `run-all` job. This leads to less duplicated work e.g. when both FileChanged and a EnvCommonChanged should trigger a plan in the same unit. When [consolidate_added_or_changed](/2.0/reference/pipelines/configurations-as-code/api#consolidate_added_or_changed) is enabled this will include Module Changed / Added jobs.

This behavior will likely become the default in a major release of Pipelines but is currently opt-in due to being a breaking change to functionality.
</li>
<li>
**Default Value**: Disabled
</li>
<li>**How to Enable**: Set to `"true"`</li>
</ul>

#### `PIPELINES_FEATURE_EXPERIMENT_COLOCATED_FILE_UNIT_CHANGE_DETECTION`
<ul>
<li>
Enables changes to files within a Terragrunt Unit to be detected as a ModuleChanged job instead of a FileChanged job. A Terragrunt Unit is any directory excluding the root of the repository containing a `terragrunt.hcl` file.

E.g. given a repository containing the following files:
```
tags.yml
dir1/terragrunt.hcl
dir1/myvars.json
```

When this flag is enabled Pipelines will detect changes to `dir1/myvars.json` as a ModuleChanged for `dir1` and run Terragrunt Plan/Apply for this directory. While `tags.yml` will be detected as as a FileChanged event and Pipelines will run Terragrunt with [queue-include-units-reading](https://terragrunt.gruntwork.io/docs/reference/cli-options/#queue-include-units-reading) for this file.

This behavior will likely become the default in a major release of Pipelines but is currently opt-in due to being a breaking change to functionality.
</li>
<li>
**Default Value**: Disabled
</li>
<li>
**How to Enable**: Set to `"true"`
</li>
</ul>

#### `PIPELINES_FEATURE_EXPERIMENT_MINIMIZE_BLAST_RADIUS`
<ul>
<li>
Enables Terragrunt features to reduce the potential changes during a run-all. Terragrunt [queue-strict-include](https://terragrunt.gruntwork.io/docs/reference/cli-options/#queue-strict-include) and [queue-exclude-external](https://terragrunt.gruntwork.io/docs/reference/cli-options/#queue-exclude-external) are enabled by default which exclude dependencies from being planned/applied during run-all, and closer matches the behavior of a single unit change.

This behavior will likely become the default in a major release of Pipelines but is currently opt-in due to being a breaking change to functionality.
</li>
<li>
**Default Value**: Disabled
</li>
<li>
**How to Enable**: Set to `"true"`
</li>
</ul>

#### `PIPELINES_FEATURE_TERRAGRUNT_INCLUDE_UNITS_READING`
<ul>
<li>
Enables FileChanged jobs where changes to non HCL files are executed by Terragrunt using [queue-include-units-reading](https://terragrunt.gruntwork.io/docs/reference/cli-options/#queue-include-units-reading).

This is a break-glass feature flag and can be used to disable this functionality if it is causing issues.
</li>
<li>
**Default Value**: Enabled if the detected Terragrunt version supports [queue-include-units-reading](https://terragrunt.gruntwork.io/docs/reference/cli-options/#queue-include-units-reading)
</li>
<li>
**How to Disable**: Set to `"false"`
</li>
</ul>

#### `PIPELINES_FEATURE_TERRAGRUNT_STACK_GENERATE`
<ul>
<li>
Enables native Terragrunt stack support using commands like `terragrunt stack generate`.

This is a break-glass feature flag and can be used to disable this functionality if it is causing issues.
</li>
<li>
**Default Value**: Enabled if the detected Terragrunt version supports [stacks](https://terragrunt.gruntwork.io/docs/reference/cli-options/#stack-commands)
</li>
<li>
**How to Disable**: Set to `"false"`
</li>
</ul>