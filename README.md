# groovy-script-useful-jenkins
Recollection of useful groovy script for troubleshooting Jenkins issues.

## List specific type of jobs

```
def jobs = hudson.model.Hudson.instance.items

jobs.each { job ->
    if (job instanceof org.jenkinsci.plugins.workflow.job.WorkflowJob)
    	println("${job.name}\n")
}
```

## List specific types of items

```
Jenkins.instance.getAllItems(com.cloudbees.opscenter.server.model.SharedSlave.class)
```

## Iterate through Nodes

```
import hudson.util.*;
Jenkins jenkins = Jenkins.getInstance();
List<Node> nodes = jenkins.getNodes();
for (Node node : nodes) {
  println("Node name: " + node.getNodeName());
  println("Executors: " + node.getNumExecutors());
  Computer computer = node.toComputer();
  RunList<? extends Run> runList = computer.getBuilds();
  for (Run run : runList) {
    println(run.getTimestampString() + ": " + run.getFullDisplayName());
  }
}
```

## Iterate all the builds inside a Jenkins instance

```
import hudson.util.*;

Jenkins jenkins = Jenkins.getInstance();
List<hudson.model.Item> allItems = jenkins.getAllItems();

for (Item item : allItems) {
  println("Item Full Name: " + item.getFullName());
  if (item instanceof Job) {
    Job job = item;
    RunList<? extends Run<?,?>> builds = job.getBuilds();
    for (Run<?,?> build : builds) {
      println("Job Full Name: " + job.getFullName() + " - Build: " + build.getNumber());
    }

  }
  println("-----------------------");
}
```
## List (recursive) jobs (non pipelines) with SCMTrigger configured

```
def jobs = Jenkins.getInstance().getAllItems();

jobs.each { job -> if (job instanceof hudson.model.AbstractProject) {
    job.triggers().each { trigger -> if (trigger instanceof hudson.triggers.SCMTrigger) {
        println(job.getClass().toString() + " (" + job.getFullDisplayName() + ") -----> ${trigger.spec}\n")
      }
    }
  }
}
```
