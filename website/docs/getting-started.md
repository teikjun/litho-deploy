---
id: getting-started
title: Getting Started
---

## Adding Litho to your Project (Buck)

You can include Litho to your Android project via Buck by adding the following to your `BUCK` file:

```python
android_prebuilt_aar(
    name = "litho",
    aar = ":litho-core.aar",
    visibility = ["PUBLIC"],
)

remote_file(
    name = "litho-core.aar",
    sha1 = "sha1here",
    url = "mvn:com.facebook.litho:litho-core:aar:{{site.litho-version}}",
)

prebuilt_jar(
    name = "litho-annotation",
    binary_jar = ":litho-annotation.jar",
    visibility = ["PUBLIC"],
)

remote_file(
    name = "litho-processor.jar",
    sha1 = "sha1here",
    url = "mvn:com.facebook.litho:litho-processor:jar:{{site.litho-version}}",
)

prebuilt_jar(
    name = "litho-processor",
    binary_jar = ":litho-processor.jar",
    visibility = ["PUBLIC"],
)

remote_file(
    name = "litho-annotation.jar",
    sha1 = "sha1here",
    url = "mvn:com.facebook.litho:litho-annotation:jar:{{site.litho-version}}",
)

android_prebuilt_aar(
    name = "litho-widget",
    aar = ":litho-widget.aar",
    visibility = ["PUBLIC"],
)

remote_file(
    name = "litho-widget.aar",
    sha1 = "sha1here",
    url = "mvn:com.facebook.litho:litho-widget:aar:{{site.litho-version}}",
)

android_library(
    ...
    # Your target here
    ...
    annotation_processor_deps = [
        ":litho-annotation",
        ":litho-processor",
    ],
    annotation_processors = [
        "com.facebook.litho.specmodels.processor.ComponentsProcessor",
    ],
    provided_deps = [
        "litho-annotation",
    ],
    deps = [
        ":litho",
        ":litho-widget",
        ...
    ]
)
```

## Adding Sections to your Project


Litho comes with an optional library called Sections for declaratively building lists. You can include Sections by adding the following additional dependencies to your `BUCK` file:

```python
android_prebuilt_aar(
    name = "litho-sections",
    aar = ":litho-sections-core.aar",
    visibility = ["PUBLIC"],
)

remote_file(
    name = "litho-sections-core.aar",
    sha1 = "sha1here",
    url = "mvn:com.facebook.litho:litho-sections-core:aar:{{site.litho-version}}",
)

prebuilt_jar(
    name = "litho-sections-annotation",
    binary_jar = ":litho-sections-annotation.jar",
    visibility = ["PUBLIC"],
)

remote_file(
    name = "litho-sections-processor.jar",
    sha1 = "sha1here",
    url = "mvn:com.facebook.litho:litho-sections-processor:jar:{{site.litho-version}}",
)

prebuilt_jar(
    name = "litho-sections-processor",
    binary_jar = ":litho-sections-processor.jar",
    visibility = ["PUBLIC"],
)

remote_file(
    name = "litho-sections-annotation.jar",
    sha1 = "sha1here",
    url = "mvn:com.facebook.litho:litho-sections-annotation:jar:{{site.litho-version}}",
)

android_prebuilt_aar(
    name = "litho-sections-widget",
    aar = ":litho-sections-widget.aar",
    visibility = ["PUBLIC"],
)

remote_file(
    name = "litho-sections-widget.aar",
    sha1 = "sha1here",
    url = "mvn:com.facebook.litho:litho-sections-widget:aar:{{site.litho-version}}",
)

```
Then modify your `android_library` target as such:

```python
android_library(
    ...
    # Your target here
    ...
    annotation_processor_deps = [
        ":litho-annotation",
        ":litho-processor",
        ":litho-sections-annotations",
        ":litho-sections-processor",
    ],
    annotation_processors = [
        "com.facebook.litho.specmodels.processor.ComponentsProcessor",
        "com.facebook.litho.specmodels.processor.sections.SectionsComponentProcessor",
    ],
    provided_deps = [
        "litho-annotations",
        "litho-sections-annotations",
    ],
    deps = [
        ":litho",
        ":litho-widget",
        ":litho-sections",
        ":litho-sections-widget",
        ...
    ]
)
```

## Adding Litho to your Project (Gradle Java)

We publish the Litho artifacts to Bintray's JCenter. To include Litho to your
Android project, make sure you include the reference to the repository in your `build.gradle` file:

```groovy
repositories {
  jcenter()
}
```

Then add the dependencies like this:

```groovy
dependencies {
  // ...
  // Litho
  implementation 'com.facebook.litho:litho-core:{{site.litho-version}}'
  implementation 'com.facebook.litho:litho-widget:{{site.litho-version}}'

  annotationProcessor 'com.facebook.litho:litho-processor:{{site.litho-version}}'

  // SoLoader
  implementation 'com.facebook.soloader:soloader:{{site.soloader-version}}'

  // For integration with Fresco
  implementation 'com.facebook.litho:litho-fresco:{{site.litho-version}}'

  // For testing
  testImplementation 'com.facebook.litho:litho-testing:{{site.litho-version}}'
}
```

## Adding Sections to your Project

Litho comes with an optional library called Sections for declaratively building lists. You can include Sections by adding the following additional dependencies to your `build.gradle` file:
```groovy
dependencies {

  // Sections
  implementation 'com.facebook.litho:litho-sections-core:{{site.litho-version}}'
  implementation 'com.facebook.litho:litho-sections-widget:{{site.litho-version}}'
  compileOnly 'com.facebook.litho:litho-sections-annotations:{{site.litho-version}}'

  annotationProcessor 'com.facebook.litho:litho-sections-processor:{{site.litho-version}}'
}
```

## Using Snapshot releases

> IMPORTANT: This will break and may set your house on fire. Snapshots are unsigned and
  automatically published by our CI system. Use them for testing purposes only.

First, add the Sonatype Snapshots repository to your gradle config:

```groovy
repositories {
  maven { url "https://oss.sonatype.org/content/repositories/snapshots/" }
}
```

Then you can access the snapshot versions of all Litho artifacts that we
publish:

```groovy
dependencies {
  // ...
  // Litho
  implementation 'com.facebook.litho:litho-core:{{site.litho-snapshot-version}}'
  implementation 'com.facebook.litho:litho-widget:{{site.litho-snapshot-version}}'

  annotationProcessor 'com.facebook.litho:litho-processor:{{site.litho-snapshot-version}}'

  // SoLoader
  implementation 'com.facebook.soloader:soloader:{{site.soloader-version}}'

  // For integration with Fresco
  implementation 'com.facebook.litho:litho-fresco:{{site.litho-snapshot-version}}'

  // For testing
  testImplementation 'com.facebook.litho:litho-testing:{{site.litho-snapshot-version}}'
}
```

## Adding Litho to your Kotlin Project (Gradel Kotlin)

> IMPORTANT: Kotlin support for Litho is experimental at this point.

In order to use Litho's annotation processor, you need to opt in to the Kotlin KAPT plugin at the
top of your application's `build.gradle` file:

```groovy
apply plugin: 'kotlin-kapt'
```

We publish the Litho artifacts to Bintray's JCenter. To include Litho to your
Android project, make sure you include the reference to the repository in your `build.gradle` file:

```groovy
repositories {
  jcenter()
}
```

Then add the dependencies like this:

```groovy
dependencies {
  // ...
  // Litho
  implementation 'com.facebook.litho:litho-core:{{site.litho-version}}'
  implementation 'com.facebook.litho:litho-widget:{{site.litho-version}}'

  kapt 'com.facebook.litho:litho-processor:{{site.litho-version}}'

  // SoLoader
  implementation 'com.facebook.soloader:soloader:{{site.soloader-version}}'

  // For integration with Fresco
  implementation 'com.facebook.litho:litho-fresco:{{site.litho-version}}'

  // For testing
  testImplementation 'com.facebook.litho:litho-testing:{{site.litho-version}}'
}
```

## Adding Sections to your Project

Litho comes with an optional library called Sections for declaratively building lists. You can include Sections by adding the following additional dependencies to your `build.gradle` file:
```groovy
dependencies {

  // Sections
  implementation 'com.facebook.litho:litho-sections-core:{{site.litho-version}}'
  implementation 'com.facebook.litho:litho-sections-widget:{{site.litho-version}}'
  compileOnly 'com.facebook.litho:litho-sections-annotations:{{site.litho-version}}'

  kapt 'com.facebook.litho:litho-sections-processor:{{site.litho-version}}'
}
```

## Using Snapshot releases

> IMPORTANT: This will break and may set your house on fire. Snapshots are unsigned and
  automatically published by our CI system. Use them for testing purposes only.

First, add the Sonatype Snapshots repository to your gradle config:

```groovy
repositories {
  maven { url "https://oss.sonatype.org/content/repositories/snapshots/" }
}
```

Then you can access the snapshot versions of all Litho artifacts that we
publish:

```groovy
dependencies {
  // ...
  // Litho
  implementation 'com.facebook.litho:litho-core:{{site.litho-snapshot-version}}'
  implementation 'com.facebook.litho:litho-widget:{{site.litho-snapshot-version}}'

  kapt 'com.facebook.litho:litho-processor:{{site.litho-snapshot-version}}'

  // SoLoader
  implementation 'com.facebook.soloader:soloader:{{site.soloader-version}}'

  // For integration with Fresco
  implementation 'com.facebook.litho:litho-fresco:{{site.litho-snapshot-version}}'

  // For testing
  testImplementation 'com.facebook.litho:litho-testing:{{site.litho-snapshot-version}}'
}
```

## Testing your Installation (Java)

You can test your install by adding a view created with Litho to an activity.

First, initialize `SoLoader`. Litho has a dependency on [SoLoader](https://github.com/facebook/SoLoader) to help load native libraries provided by the underlying layout engine, [Yoga](https://yogalayout.com/docs/). Your `Application` class is a good place to do this:

```java
[MyApplication.java]
public class MyApplication extends Application {

  @Override
  public void onCreate() {
    super.onCreate();

    SoLoader.init(this, false);
  }
}
```

Then, add a predefined Litho `Text` widget to an activity that displays "Hello World!":

```java
[MyActivity.java]
import com.facebook.litho.ComponentContext;
import com.facebook.litho.LithoView;

public class MyActivity extends Activity {

  @Override
  public void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);

    final ComponentContext c = new ComponentContext(this);

    final LithoView lithoView = LithoView.create(
    	this /* context */,
    	Text.create(c)
            .text("Hello, World!")
            .textSizeDip(50)
            .build());

    setContentView(lithoView);
  }
}
```

Now, when you run the app you should see "Hello World!" displayed on the screen.

## Testing your Installation (Kotlin)

You can test your install by adding a view created with Litho to an activity.

First, initialize `SoLoader`. Litho has a dependency on [SoLoader](https://github.com/facebook/SoLoader) to help load native libraries provided by the underlying layout engine, [Yoga](https://yogalayout.com/docs/). Your `Application` class is a good place to do this:

```kotlin
[MyApplication.kt]
class MyApplication: Application() {

  override fun onCreate() {
    super.onCreate()
    SoLoader.init(this, false)
  }
}
```

Then, add a predefined Litho `Text` widget to an activity that displays "Hello World!":

```kotlin
[MyActivity.kt]
import com.facebook.litho.ComponentContext
import com.facebook.litho.LithoView

class MyActivity : AppCompatActivity() {

  override fun onCreate(savedInstanceState: Bundle?) {
    super.onCreate(savedInstanceState)

    val c = ComponentContext(this)

    val lithoView = LithoView.create(
        this /* context */,
        Text.create(c)
            .text("Hello, World!")
            .textSizeDip(50)
            .build())

    setContentView(lithoView)
  }
}
```

Now, when you run the app you should see "Hello World!" displayed on the screen.
