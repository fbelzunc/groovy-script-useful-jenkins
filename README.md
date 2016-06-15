# groovy-script-useful-jenkins
Recollection of useful groovy script for troubleshooting Jenkins issues.

## List specific type of jobs

def jobs = hudson.model.Hudson.instance.items

```
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