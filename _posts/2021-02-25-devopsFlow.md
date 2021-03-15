---
title: Debateops. Por qué este blog.
header:
  overlay_image: /assets/images/environments.png
category:
  - debateops
tags:
  - debateops
  - agile
  - devops
---

# DevOps process flow 

devop philosophy in this project:

1. Automation: Automate everything, The tests and their reports are created automatically, if they do not pass, you cannot continue. The manuel step is to merge PR in github.
2. Iteration: Jenkins and github complement each other to show where we are and how we are going.
3. Continuous improvement: Continuously test, tests are in the same repository and the tests are passed every day. 
4. Collaboration: Everyone sees the same repository and everyone sees project progress, and if something goes wrong it's everyone's fault.

![devops_teams_test](/assets/images/circle_colors.png)

We have four environments, each with its branches, its different tests and responsibilities.
The code flows between the different branches of github, and when a PR is created it is tested in the corresponding environment, and only if it passes all the tests and is successful, the right person on the team approves the PR, moving to the next level.

![devops_environments](/assets/images/environments.png)

**Developer**: they solve US or bugs modifying code with commits, then PRs are created on github. Due to the github hook, the associated jobs are executed, showing in github if they pass the tests, sonar, ... another developer seeing the results of the jobs, and checking the code merges the branch.

    1. branch: featureX bugX
    2. jobs: 
        * compile
        * unit test
        * code coverage
        * sonar
 
**QA**: every night the develop branch is deployed to the QA environment. All the integration tests are passed and reports of coverage of functionality is created.
       We verify that nothing has been broken. QA environmentis a real environment, although it doesn't need to look like production.

    1. branch: develop
    2. jobs: 
        * smoke test
        * sanity test
        * accept test
        
    When the QA team has created enough tests, develop branch is merged to the release/X.


**Security**: stage is an environment similar to the production one, where it is going to validate how the application reacts to unforeseen, adverse situations.

    1. branch: release/X
    2. jobs:
        * security test
        * performance test
        * HA test

    Only if all the jobs have passed is the release accepted and it is available for deployment. This operation is planned because they are very expensive tests and equipment that is not usually dedicated to a single project.

**Operations**: production environment with data and users. Measure actual use and user satisfaction and problems
    
    1. branch: master
    2. jobs: monitor traces
    monitor status of servers (cpu, disk, ...)
    monitor user operations
    Only here is where you see if all the work done has been useful, suggestions are created to improve development, ...

