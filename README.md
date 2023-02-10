# actions_test
Tests actions


I'm just checking if there is an option for malicious people to run whatever they want on github/self-hosted runners and retrieve like secrets and whatever. Because it seems to me that for instance a test could be configured with a secret value, and then you just kinda extract it in a test and thats that. 

## Notes

Template variables get filled before any runs happens
    * Probably in Set up Job part
    * se get instantiated when it sees a jobs-token
        * then gets wwhere it should run, possibly more args and then executes steps

    * so how does it do the job.status? It must be dynamically updated, atleast the job part
* There are sets of preconfigured runners that Girhub publishes at (https://github.com/actions/starter-workflows)[https://github.com/actions/starter-workflows]

Workflows can run on any event, not just pushes. So for instance creating an issue. A workflow runs jobs, sequentiall or parallel, which has steps in it. 
    * steps can be actions which are reusable  (so it can call outside of its file?)
    * these are actions, and are called by the uses: keyword
    * We can add actions by creating s .github/actions/ folder and they can be referenced there. From the marketplace on github there are things which we can add, and probably the action/checkout things are automaticaly imported in this way.

 * List of events that can be hooked (https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows)[https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows]
    * can workflows create events? -- infinite loop


Varibles are can be set by inputs to actions, or env: keyword (obvi)

Since we are in the workspace of the repo we are also free to run any shell-script or similar in the repo.

Expression looks like ${{ expression }}
Github warns here
>Warning: When creating workflows and actions, you should always consider whether your code might execute untrusted input from possible attackers. Certain contexts should be treated as untrusted input, as an attacker could insert their own malicious content. For more information, see "Understanding the risk of script injections."

Example:
    * env:
        MyValue: ${{ 0xff }}

github.token is a sensitive api-token, it gets default masked, from the log, but is there. It has access to the repository, on behalf of GitHub Apps

env variables can be set on steps, jobs or workflows, and are accessible as the normal $Env_name in all cases. It can albe be accessed through the contexts aka ${{ workflow }} for instance


In settings->secrets and variables-> Actions you can set configuration variables for your repository - this seems weird? they surely can be set in the workflow file as well?
Configuration variables are not environment variables, they are accessbile in the vars context


## Exfilling data works just fine

It is possible to just curl from the run and get data



## Reconing on runner-machine

We can read syslog and see that it was provisioned yesterday (or logs have been deleted from before)
we can see that our run was executed there. There is some pod-related data, including the generation of ssh-keys
This is probably why they say to set secrets, so that the secrets in the logs are masked out.


## self-hosted runner

This is your own machine and it seems like it will just run whatever is in the workflow, so I guess it is possible to just take over the machines of anyone using this?
