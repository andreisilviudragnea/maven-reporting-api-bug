# maven-reporting-api-bug

Run `./mvnw clean package site` to reproduce the bug.

```
[WARNING] An issue has occurred with scoverage-maven-plugin:1.4.11:report-only report, skipping LinkageError Receiver class org.scoverage.plugin.SCoverageReportOnlyMojo does not define or inherit an implementation of the resolved method 'abstract void generate(org.apache.maven.doxia.sink.Sink, java.util.Locale)' of interface org.apache.maven.reporting.MavenReport., please report an issue to Maven dev team.
java.lang.AbstractMethodError: Receiver class org.scoverage.plugin.SCoverageReportOnlyMojo does not define or inherit an implementation of the resolved method 'abstract void generate(org.apache.maven.doxia.sink.Sink, java.util.Locale)' of interface org.apache.maven.reporting.MavenReport.
    at org.apache.maven.plugins.site.render.ReportDocumentRenderer.renderDocument (ReportDocumentRenderer.java:235)
    at org.apache.maven.doxia.siterenderer.DefaultSiteRenderer.render (DefaultSiteRenderer.java:348)
    at org.apache.maven.plugins.site.render.SiteMojo.renderLocale (SiteMojo.java:194)
    at org.apache.maven.plugins.site.render.SiteMojo.execute (SiteMojo.java:143)
    at org.apache.maven.plugin.DefaultBuildPluginManager.executeMojo (DefaultBuildPluginManager.java:137)
    at org.apache.maven.lifecycle.internal.MojoExecutor.doExecute (MojoExecutor.java:301)
    at org.apache.maven.lifecycle.internal.MojoExecutor.execute (MojoExecutor.java:211)
    at org.apache.maven.lifecycle.internal.MojoExecutor.execute (MojoExecutor.java:165)
    at org.apache.maven.lifecycle.internal.MojoExecutor.execute (MojoExecutor.java:157)
    at org.apache.maven.lifecycle.internal.LifecycleModuleBuilder.buildProject (LifecycleModuleBuilder.java:121)
    at org.apache.maven.lifecycle.internal.LifecycleModuleBuilder.buildProject (LifecycleModuleBuilder.java:81)
    at org.apache.maven.lifecycle.internal.builder.singlethreaded.SingleThreadedBuilder.build (SingleThreadedBuilder.java:56)
    at org.apache.maven.lifecycle.internal.LifecycleStarter.execute (LifecycleStarter.java:127)
    at org.apache.maven.DefaultMaven.doExecute (DefaultMaven.java:294)
    at org.apache.maven.DefaultMaven.doExecute (DefaultMaven.java:192)
    at org.apache.maven.DefaultMaven.execute (DefaultMaven.java:105)
    at org.apache.maven.cli.MavenCli.execute (MavenCli.java:960)
    at org.apache.maven.cli.MavenCli.doMain (MavenCli.java:293)
    at org.apache.maven.cli.MavenCli.main (MavenCli.java:196)
    at jdk.internal.reflect.NativeMethodAccessorImpl.invoke0 (Native Method)
    at jdk.internal.reflect.NativeMethodAccessorImpl.invoke (NativeMethodAccessorImpl.java:62)
    at jdk.internal.reflect.DelegatingMethodAccessorImpl.invoke (DelegatingMethodAccessorImpl.java:43)
    at java.lang.reflect.Method.invoke (Method.java:566)
    at org.codehaus.plexus.classworlds.launcher.Launcher.launchEnhanced (Launcher.java:282)
    at org.codehaus.plexus.classworlds.launcher.Launcher.launch (Launcher.java:225)
    at org.codehaus.plexus.classworlds.launcher.Launcher.mainWithExitCode (Launcher.java:406)
    at org.codehaus.plexus.classworlds.launcher.Launcher.main (Launcher.java:347)
    at jdk.internal.reflect.NativeMethodAccessorImpl.invoke0 (Native Method)
    at jdk.internal.reflect.NativeMethodAccessorImpl.invoke (NativeMethodAccessorImpl.java:62)
    at jdk.internal.reflect.DelegatingMethodAccessorImpl.invoke (DelegatingMethodAccessorImpl.java:43)
    at java.lang.reflect.Method.invoke (Method.java:566)
    at org.apache.maven.wrapper.BootstrapMainStarter.start (BootstrapMainStarter.java:47)
    at org.apache.maven.wrapper.WrapperExecutor.execute (WrapperExecutor.java:156)
    at org.apache.maven.wrapper.MavenWrapperMain.main (MavenWrapperMain.java:72)

```

Downgrade `<maven-site-plugin.version>3.11.0</maven-site-plugin.version>` to
`<maven-site-plugin.version>3.10.0</maven-site-plugin.version>`, run `./mvnw clean package site` 
and the bug goes away.

https://github.com/apache/maven-site-plugin/pull/69 is the PR which introduced the
update to `org.apache.maven.reporting:maven-reporting-api:3.1.0` in `org.apache.maven.plugins:maven-site-plugin:3.11.0`. 
