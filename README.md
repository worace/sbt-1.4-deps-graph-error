# SBT Built-in dependency graph plugin error

This is an example project showing an SBT dependency graph plugin error that I ran into with the new built-in version of that plugin in sbt 1.4.0.

Errors similar to this seem to have popped up a few times in the sbt and sbt-dependency-graph issue trackers, e.g. [sbt#4688](https://github.com/sbt/sbt/issues/4688).

Error:

```
sbt 'whatDependsOn io.circe circe-core 0.11.2'
[info] welcome to sbt 1.4.0 (Oracle Corporation Java 1.8.0_201)
[info] loading settings for project global-plugins from plugins.sbt ...
[info] loading global plugins from /home/horace/.sbt/1.0/plugins
[info] loading project definition from /home/horace/scratch/dep-graph-test/project
[info] loading settings for project root from build.sbt ...
[info] set current project to dep graph test (in build file:/home/horace/scratch/dep-graph-test/)
[error] java.lang.NoSuchMethodError: sbt.internal.LibraryManagement$.cachedUpdate(Lsbt/librarymanagement/DependencyResolution;Lsbt/librarymanagement/ModuleDescriptor;Lsbt/util/CacheStoreFactory;Ljava/lang/String;Lsbt/librarymanagement/UpdateConfiguration;Lscala/Function1;ZZZLsbt/librarymanagement/UnresolvedWarningConfiguration;Lsbt/librarymanagement/EvictionWarningOptions;ZLsbt/internal/librarymanagement/CompatibilityWarningOptions;Lsbt/util/Logger;)Lsbt/librarymanagement/UpdateReport;
[error]         at sbt.dependencygraph.DependencyGraphSbtCompat$.$anonfun$updateTask$5(DependencyGraphSbtCompat.scala:61)
[error]         at scala.Function1.$anonfun$compose$1(Function1.scala:49)
[error]         at sbt.internal.util.$tilde$greater.$anonfun$$u2219$1(TypeFunctions.scala:62)
[error]         at sbt.std.Transform$$anon$4.work(Transform.scala:68)
[error]         at sbt.Execute.$anonfun$submit$2(Execute.scala:282)
[error]         at sbt.internal.util.ErrorHandling$.wideConvert(ErrorHandling.scala:23)
[error]         at sbt.Execute.work(Execute.scala:291)
[error]         at sbt.Execute.$anonfun$submit$1(Execute.scala:282)
[error]         at sbt.ConcurrentRestrictions$$anon$4.$anonfun$submitValid$1(ConcurrentRestrictions.scala:265)
[error]         at sbt.CompletionService$$anon$2.call(CompletionService.scala:64)
[error]         at java.util.concurrent.FutureTask.run(FutureTask.java:266)
[error]         at java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:511)
[error]         at java.util.concurrent.FutureTask.run(FutureTask.java:266)
[error]         at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1149)
[error]         at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:624)
[error]         at java.lang.Thread.run(Thread.java:748)
[error] (ivyReport / update) java.lang.NoSuchMethodError: sbt.internal.LibraryManagement$.cachedUpdate(Lsbt/librarymanagement/DependencyResolution;Lsbt/librarymanagement/ModuleDescriptor;Lsbt/util/CacheStoreFactory;Ljava/lang/String;Lsbt/librarymanagement/UpdateConfiguration;Lscala/Function1;ZZZLsbt/librarymanagement/UnresolvedWarningConfiguration;Lsbt/librarymanagement/EvictionWarningOptions;ZLsbt/internal/librarymanagement/CompatibilityWarningOptions;Lsbt/util/Logger;)Lsbt/librarymanagement/UpdateReport;
[error] Total time: 0 s, completed Oct 5, 2020 7:43:33 AM
```

Note that other commands like `sbt dependencyTree` still seem to work out of the box.

Also, going back to the external dependency-graph plugin also seems to restore the `whatDependsOn` functionality:

(In `project/plugins.sbt`):

```
// Uncomment this to fix 'whatDependsOn' errors
// addSbtPlugin("net.virtual-void" % "sbt-dependency-graph" % "0.10.0-RC1")
```
