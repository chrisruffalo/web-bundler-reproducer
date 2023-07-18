# Web Bundler Error Reproducer

Reproduces [this issue](https://github.com/quarkiverse/quarkus-web-bundler/pull/46#issuecomment-1637633266). This
only seems to need one submodule to go wrong. In the full projects I have a separate bom module as well as multiple
modules with dependencies but this is the minimal reproducer. I added the flatten-pom plugin because I use it with the
other projects.

The thrown exception is:
```shell
[ERROR] Failed to execute goal io.quarkus.platform:quarkus-maven-plugin:3.2.0.Final:build (default) on project web-bundler-ui-1: Failed to build quarkus application: io.quarkus.builder.BuildException: Build failure: Build failed due to errors
[ERROR]         [error]: Build step io.quarkiverse.web.bundler.deployment.staticresources.GeneratedStaticResourcesProcessor#processStaticFiles threw an exception: java.lang.NullPointerException: Cannot invoke "io.quarkus.bootstrap.workspace.WorkspaceModule.getBuildDir()" because the return value of "io.quarkus.maven.dependency.ResolvedDependency.getWorkspaceModule()" is null
[ERROR]         at io.quarkiverse.web.bundler.deployment.staticresources.GeneratedStaticResourcesProcessor.getBuildDirectory(GeneratedStaticResourcesProcessor.java:110)
[ERROR]         at io.quarkiverse.web.bundler.deployment.staticresources.GeneratedStaticResourcesProcessor.processStaticFiles(GeneratedStaticResourcesProcessor.java:38)
[ERROR]         at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
[ERROR]         at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:77)
[ERROR]         at java.base/jdk.internal.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
[ERROR]         at java.base/java.lang.reflect.Method.invoke(Method.java:568)
[ERROR]         at io.quarkus.deployment.ExtensionLoader$3.execute(ExtensionLoader.java:909)
[ERROR]         at io.quarkus.builder.BuildContext.run(BuildContext.java:282)
[ERROR]         at org.jboss.threads.ContextHandler$1.runWith(ContextHandler.java:18)
[ERROR]         at org.jboss.threads.EnhancedQueueExecutor$Task.run(EnhancedQueueExecutor.java:2513)
[ERROR]         at org.jboss.threads.EnhancedQueueExecutor$ThreadBody.run(EnhancedQueueExecutor.java:1538)
[ERROR]         at java.base/java.lang.Thread.run(Thread.java:833)
[ERROR]         at org.jboss.threads.JBossThread.run(JBossThread.java:501)
[ERROR] -> [Help 1]
[ERROR]
[ERROR] To see the full stack trace of the errors, re-run Maven with the -e switch.
[ERROR] Re-run Maven using the -X switch to enable full debug logging.
[ERROR]
[ERROR] For more information about the errors and possible solutions, please read the following articles:
[ERROR] [Help 1] http://cwiki.apache.org/confluence/display/MAVEN/MojoExecutionException
[ERROR]
[ERROR] After correcting the problems, you can resume the build with the command
[ERROR]   mvn <args> -rf :sample-ui
```
