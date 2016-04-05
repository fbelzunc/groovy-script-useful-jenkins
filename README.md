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
