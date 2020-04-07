# Forks

## Typical architecture
Using forks, we have the following `git` project architecture. 
|----------------------|
|                      |
|     the-project      |
| (upstream - Github)  |
|----------------------|
        |
        |
        |--------------------------------------------------------------------------------
        |                                       |                                       |
|------------------------------|    |------------------------------|   |------------------------------|
|                              |    |                              |   |                              |
|     Clovis/the-project       |    |     Raph/the-project         |   |     Camille/the-project      |
| (distant - Github (fork))    |    |  (distant - Github (fork))   |   | (distant - Github (fork)) |
|------------------------------|    |------------------------------|   |------------------------------|
        |                                       |                                       |
        |                                       |                                       |
|------------------------------|    |------------------------------|   |------------------------------|
|                              |    |                              |   |                              |
|     the-project              |    |     the-project              |   |     the-project              |
|  (Clovis - local))           |    |  (Raph - local)              |   |  (Camille - local)           |
|------------------------------|    |------------------------------|   |------------------------------|


To submit new code to the upstream, the team must use "Merge Requests" (sometimes called "Pull Resuests"). A developper can do anything with his/her fork. Pull resuests contain the only code that will be merged into the upstream.

Only the integrator or the project's leader can touch the upstream directly, and should do so only for exceptionzl cases. They should have their own fork for development.
# Simplified architecture

|------------------------------|
|                              |
|     the-project              |
| (distant - Github (Org))     |
|------------------------------|
        |
        |--------------------------------------------------------------------------------
        |                                       |                                       |
|------------------------------|    |------------------------------|   |------------------------------|
|                              |    |                              |   |                              |
|     the-project              |    |     the-project              |   |     the-project              |
|  (Clovis - local))           |    |  (Raph - local)              |   |  (Camille - local)           |
|------------------------------|    |------------------------------|   |------------------------------|

This `git` process simplifies things for small teams with a fixed number of collaborators. But his can complicate things by causing merge conflicts or branch conflicts. Everybody should work on seperate branches as much as possible. 

Only the integrator or the project leader should touch to the remote's master branch, and should do so only for exceptional cases. They should work on their own branches for development purposes. 

