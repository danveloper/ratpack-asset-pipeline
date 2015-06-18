## Ratpack Asset-Pipeline

This module provides runtime for both development and production to the Ratpack framework for rendering files compiled by Asset-Pipeline. This should be paired with the asset-pipeline-gradle plugin appropriately

**NOTE**: Version `2.3.0` has resulted in a change of config and asset location. Please read the documentation below if needing to upgrade.

```groovy
buildscript {
  repositories {
    jcenter()
    mavenCentral()
  }
  dependencies {
    classpath 'com.bertramlabs.plugins:asset-pipeline-gradle:2.3.2'
    //Example additional LESS support
    //classpath 'com.bertramlabs.plugins:less-asset-pipeline:2.3.0'
  }
}

apply plugin: 'asset-pipeline'

dependencies {
	compile 'com.bertramlabs.plugins:ratpack-asset-pipeline:2.3.2'
	//Example additional LESS support
    //provided 'com.bertramlabs.plugins:less-asset-pipeline:2.3.0'
}

```
Also add the Module to your registry

```groovy
import asset.pipeline.ratpack.AssetPipelineModule;

bindings {
  module new AssetPipelineModule()
}
```

Or if you want to configure the module

```groovy
import asset.pipeline.ratpack.AssetPipelineModule;
import ratpack.config.ConfigData;

bindings {
  ConfigData configData = ConfigData.of().sysProps().build()
    moduleConfig(new AssetPipelineModule(), configData.get(AssetPipelineModule.Config))
}
```

Now you could for example change the less compiler mode with the system property `-Dratpack.assets.less.compiler=standard`

In your `src/assets` folder create organizational subfolders i.e. `src/assets/javascripts` or `src/assets/stylesheets`.

You can reference these files in your html templates via `/assets/application.js`. The md5 url replacement work is still in progress as Ratpack spec gets finalized.

### Things to be Done

* Url replacements for templates
* Testing