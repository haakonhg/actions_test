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

 * List of events that can be hooked (https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows)[https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows]
