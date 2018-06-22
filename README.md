# java-ls-repro

This repository reproduces an error in [vs-code-java](https://github.com/redhat-developer/vscode-java) language server/client in combination with maven.

**Steps to reproduce**
1. Open in vscode
2. Open a terminal
3. `cd my-app`
5. Open `src\main\java\com\mycompany\app\App.java`
6. Make a change (add a line) hit Save
7. Call `mvn clean`
6. Make a change (add a line) hit Save
7. Go to new foo() -> navigate to foo (F12)
8. Red squigglies occure on `foo()` and `import com.mycompany.app.foo;`
9. Call `mvn compile`
10. Make a change (add a line) -> red squigglies go away
11. Hit save -> Red squigglies come back, even if build is successfully
12. VS-Code/Language server/Language client never recovers

**Log file**
```txt

!ENTRY org.eclipse.jdt.core 4 4 2018-06-21 16:31:41.860
!MESSAGE JavaBuilder handling CoreException
!STACK 1
org.eclipse.core.internal.resources.ResourceException(/my-app/target/classes/com/mycompany/app/App.class)[368]: java.lang.Exception: File not found: C:\f\git\foo\my-app\target\classes\com\mycompany\app\App.class.
	at org.eclipse.core.internal.resources.ResourceException.provideStackTrace(ResourceException.java:39)
	at org.eclipse.core.internal.resources.ResourceException.<init>(ResourceException.java:35)
	at org.eclipse.core.internal.localstore.FileSystemResourceManager.read(FileSystemResourceManager.java:830)
	at org.eclipse.core.internal.resources.File.getContents(File.java:277)
	at org.eclipse.jdt.internal.core.util.Util.getResourceContentsAsByteArray(Util.java:1149)
	at org.eclipse.jdt.internal.core.builder.IncrementalImageBuilder.writeClassFileCheck(IncrementalImageBuilder.java:939)
	at org.eclipse.jdt.internal.core.builder.IncrementalImageBuilder.writeClassFileContents(IncrementalImageBuilder.java:881)
	at org.eclipse.jdt.internal.core.builder.AbstractImageBuilder.writeClassFile(AbstractImageBuilder.java:871)
	at org.eclipse.jdt.internal.core.builder.AbstractImageBuilder.acceptResult(AbstractImageBuilder.java:200)
	at org.eclipse.jdt.internal.compiler.Compiler.processCompiledUnits(Compiler.java:615)
	at org.eclipse.jdt.internal.compiler.Compiler.compile(Compiler.java:472)
	at org.eclipse.jdt.internal.compiler.Compiler.compile(Compiler.java:423)
	at org.eclipse.jdt.internal.core.builder.AbstractImageBuilder.compile(AbstractImageBuilder.java:383)
	at org.eclipse.jdt.internal.core.builder.IncrementalImageBuilder.compile(IncrementalImageBuilder.java:368)
	at org.eclipse.jdt.internal.core.builder.AbstractImageBuilder.compile(AbstractImageBuilder.java:315)
	at org.eclipse.jdt.internal.core.builder.IncrementalImageBuilder.incrementalBuildLoop(IncrementalImageBuilder.java:183)
	at org.eclipse.jdt.internal.core.builder.IncrementalImageBuilder.build(IncrementalImageBuilder.java:140)
	at org.eclipse.jdt.internal.core.builder.JavaBuilder.buildDeltas(JavaBuilder.java:276)
	at org.eclipse.jdt.internal.core.builder.JavaBuilder.build(JavaBuilder.java:197)
	at org.eclipse.core.internal.events.BuildManager$2.run(BuildManager.java:795)
	at org.eclipse.core.runtime.SafeRunner.run(SafeRunner.java:42)
	at org.eclipse.core.internal.events.BuildManager.basicBuild(BuildManager.java:216)
	at org.eclipse.core.internal.events.BuildManager.basicBuild(BuildManager.java:259)
	at org.eclipse.core.internal.events.BuildManager$1.run(BuildManager.java:312)
	at org.eclipse.core.runtime.SafeRunner.run(SafeRunner.java:42)
	at org.eclipse.core.internal.events.BuildManager.basicBuild(BuildManager.java:315)
	at org.eclipse.core.internal.events.BuildManager.basicBuildLoop(BuildManager.java:367)
	at org.eclipse.core.internal.events.BuildManager.build(BuildManager.java:388)
	at org.eclipse.core.internal.events.AutoBuildJob.doBuild(AutoBuildJob.java:142)
	at org.eclipse.core.internal.events.AutoBuildJob.run(AutoBuildJob.java:232)
	at org.eclipse.core.internal.jobs.Worker.run(Worker.java:60)
!SUBENTRY 1 org.eclipse.core.resources 4 368 2018-06-21 16:31:41.861
!MESSAGE File not found: C:\f\git\foo\my-app\target\classes\com\mycompany\app\App.class.
!STACK 0
java.lang.Exception: File not found: C:\f\git\foo\my-app\target\classes\com\mycompany\app\App.class.
	at org.eclipse.core.internal.resources.ResourceException.provideStackTrace(ResourceException.java:39)
	at org.eclipse.core.internal.resources.ResourceException.<init>(ResourceException.java:35)
	at org.eclipse.core.internal.localstore.FileSystemResourceManager.read(FileSystemResourceManager.java:830)
	at org.eclipse.core.internal.resources.File.getContents(File.java:277)
	at org.eclipse.jdt.internal.core.util.Util.getResourceContentsAsByteArray(Util.java:1149)
	at org.eclipse.jdt.internal.core.builder.IncrementalImageBuilder.writeClassFileCheck(IncrementalImageBuilder.java:939)
	at org.eclipse.jdt.internal.core.builder.IncrementalImageBuilder.writeClassFileContents(IncrementalImageBuilder.java:881)
	at org.eclipse.jdt.internal.core.builder.AbstractImageBuilder.writeClassFile(AbstractImageBuilder.java:871)
	at org.eclipse.jdt.internal.core.builder.AbstractImageBuilder.acceptResult(AbstractImageBuilder.java:200)
	at org.eclipse.jdt.internal.compiler.Compiler.processCompiledUnits(Compiler.java:615)
	at org.eclipse.jdt.internal.compiler.Compiler.compile(Compiler.java:472)
	at org.eclipse.jdt.internal.compiler.Compiler.compile(Compiler.java:423)
	at org.eclipse.jdt.internal.core.builder.AbstractImageBuilder.compile(AbstractImageBuilder.java:383)
	at org.eclipse.jdt.internal.core.builder.IncrementalImageBuilder.compile(IncrementalImageBuilder.java:368)
	at org.eclipse.jdt.internal.core.builder.AbstractImageBuilder.compile(AbstractImageBuilder.java:315)
	at org.eclipse.jdt.internal.core.builder.IncrementalImageBuilder.incrementalBuildLoop(IncrementalImageBuilder.java:183)
	at org.eclipse.jdt.internal.core.builder.IncrementalImageBuilder.build(IncrementalImageBuilder.java:140)
	at org.eclipse.jdt.internal.core.builder.JavaBuilder.buildDeltas(JavaBuilder.java:276)
	at org.eclipse.jdt.internal.core.builder.JavaBuilder.build(JavaBuilder.java:197)
	at org.eclipse.core.internal.events.BuildManager$2.run(BuildManager.java:795)
	at org.eclipse.core.runtime.SafeRunner.run(SafeRunner.java:42)
	at org.eclipse.core.internal.events.BuildManager.basicBuild(BuildManager.java:216)
	at org.eclipse.core.internal.events.BuildManager.basicBuild(BuildManager.java:259)
	at org.eclipse.core.internal.events.BuildManager$1.run(BuildManager.java:312)
	at org.eclipse.core.runtime.SafeRunner.run(SafeRunner.java:42)
	at org.eclipse.core.internal.events.BuildManager.basicBuild(BuildManager.java:315)
	at org.eclipse.core.internal.events.BuildManager.basicBuildLoop(BuildManager.java:367)
	at org.eclipse.core.internal.events.BuildManager.build(BuildManager.java:388)
	at org.eclipse.core.internal.events.AutoBuildJob.doBuild(AutoBuildJob.java:142)
	at org.eclipse.core.internal.events.AutoBuildJob.run(AutoBuildJob.java:232)
	at org.eclipse.core.internal.jobs.Worker.run(Worker.java:60)

```
