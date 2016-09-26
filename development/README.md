[![](https://images.microbadger.com/badges/image/tangrui/pinpoint-development.svg)](https://microbadger.com/images/tangrui/pinpoint-development "Get your own image badge on microbadger.com")

# Usage

You can use the container like this:

```bash
$ git clone https://github.com/naver/pinpoint
$ docker run --rm -v $(pwd)/pinpoint:/pinpoint:rw -v /Users/$(whoami)/.m2:/root/.m2:rw tangrui/pinpoint-development
```

# Description

1. The first -v mount the cloned Pinpoint project volume to container's `/pinpoint` directory.
2. The second -v mount the host's Maven repository to container's `/root/.m2` directory, this will cache all the Maven artifacts instead of downloading them every time from the internet.
3. This will run the default command `mvn install -Dmaven.skip.test=true` defined in Dockerfile. If you want to run some other commands, do it like this:

```bash
$ docker run -v $(pwd)/pinpoint:/pinpoint:rw -v /Users/$(whoami)/.m2:/root/.m2:rw tangrui/pinpoint-development mvn clean install -Dmaven.skip.test=true
```

After the first time successfully build, you can change the Pinpoint project location `$(pwd)/pinpoint` to your own Pinpoint plugin project, and the build should run correctly. For example, you can use the following command to build [Pinpoint Plugin Samples](https://github.com/lioolli/pinpoint-plugin-sample):

```bash
$ git clone https://github.com/naver/pinpoint-plugin-sample
$ docker run -v $(pwd)/pinpoint-plugin-sample:/pinpoint:rw -v /Users/$(whoami)/.m2:/root/.m2:rw
```

To run the integration test, you can:

```bash
$ docker run -v $(pwd)/pinpoint-plugin-sample:/pinpoint:rw -v /Users/$(whoami)/.m2:/root/.m2:rw mvn integration-test
```

# Credits

This Dockerfile is hardly based on the excellent work of [@yous](https://github.com/yous/pinpoint-docker), but has fewer and smaller layers to pull from.
