## envoy
*   L3/L4, L7 layer proxy
*   can be used for side-car or mesh deployment pattern
*   supports http/2, static and dynamic configuration
*   request flow
```
listeners => routes =>  clusters => endpoint
```

## envoy using func-e

**func-e** is a command line tool to test different envoy versions in local machine

intall the tool
```
curl https://func-e.io/install.sh | bash -s -- -b /usr/local/bin
```

tool version
```
func-e --version
```

lists all the available envoy version
```
func-e versions -a
```

use specific envoy version
```
func-e use 1.24.0
```

run envoy
```
func-e run -c cluster.yml
```




## envoy using docker


pull the image
```
docker pull envoyproxy/envoy-dev
```

check version
```
docker run --rm envoyproxy/envoy-dev --version 
```	

validate envoy config file
```
docker run --rm -it  -v $(pwd)/helloworld.yml:/helloworld.yml envoyproxy/envoy-dev --mode validate -c helloworld.yml 
```

run envoy
```
docker run --rm -it -p 9901:9901 -p 10000:10000 -v $(pwd)/helloworld.yml:/helloworld.yml envoyproxy/envoy-dev -c helloworld.yml 
```

**online envoy config linter/validator**
```
https://envoylint.com/
```

reference:
*   https://www.envoyproxy.io/docs/envoy/latest/start/start
*   https://academy.tetrate.io/courses/take/envoy-fundamentals/lessons/28296421-1-1-what-is-envoy
*   https://github.com/tetratelabs/func-e