---
translated_page: https://github.com/PX4/Devguide/blob/master/en/test_and_ci/jenkins_ci.md
translated_sha: 95b39d747851dd01c1fe5d36b24e59ec865e323e
---

# Jenkins CI

Jenkins continuous integration server on [SITL01](http://sitl01.dronetest.io/) is used to automatically run integration tests against PX4 SITL.

## Overview

  * Involved components: Jenkins, Docker, PX4 SITL
  * Tests run inside [Docker Containers](../test_and_ci/docker.md)
  * Jenkins executes 2 jobs: one to check each PR against master, and the other to check every push on master

## Test Execution

Jenkins uses [run_container.bash](https://github.com/PX4/Firmware/blob/master/integrationtests/run_container.bash) to start the container which in turn executes [run_tests.bash](https://github.com/PX4/Firmware/blob/master/integrationtests/run_tests.bash) to compile and run the tests.

If Docker is installed the same method can be used locally:

```sh
cd <directory_where_firmware_is_cloned>
sudo WORKSPACE=$(pwd) ./Firmware/integrationtests/run_container.bash
```

## Server Setup

### Installation

See setup [script/log](https://github.com/PX4/containers/tree/master/scripts/jenkins) for details on how Jenkins got installed and maintained.

### Configuration

  * Jenkins security enabled
  * Installed plugins
    * github
    * github pull request builder
    * embeddable build status plugin
    * s3 plugin
    * notification plugin
    * collapsing console sections
    * postbuildscript
