# KubeLogs

## Description

Script for monitoring and observing logs from k8s resources.

## Usage

```shell

usage: klogs [-h] {audit,logs} ...

Utility tool for observing kubernetes resources

positional arguments:
  {audit,logs}  Commands
    audit       Audits the state of the resource specified
    logs        Prints logs from multiple resources concurrently

optional arguments:
  -h, --help    show this help message and exit

```

```shell

usage: klogs logs [-h] [-n <arg>] [-i] [-v] [-ctx <name>] [-l <number>] [-f]
                  [-hi] [-regx <^some_word$>]
                  name

positional arguments:
  name                  Resource name

optional arguments:
  -h, --help            show this help message and exit
  -n <arg>, --namespace <arg>
                        Namespace
  -i, --inverse         Does not container 'name'
  -v, --verbose         Prints commands used
  -ctx <name>, --context <name>
                        Specify which context to use based on kube-config
  -l <number>, --lines <number>
                        No of lines to take from each log. Defaults to 1000
  -f, --follow          Follows logs
  -hi, --highlight      Will highlight errors and warnings
  -regx <^some_word$>, --custom-regx <^some_word$>
                        Will highlight output based on the regx provided

```

```

usage: klogs audit [-h] [-n <arg>] [-i] [-v] [-ctx <name>] [-ma <minutes>]
                   name

positional arguments:
  name                  Resource name

optional arguments:
  -h, --help            show this help message and exit
  -n <arg>, --namespace <arg>
                        Namespace
  -i, --inverse         Does not container 'name'
  -v, --verbose         Prints commands used
  -ctx <name>, --context <name>
                        Specify which context to use based on kube-config
  -ma <minutes>, --max-age <minutes>
                        Will highlight pods that surpass the limit

```

## Examples

Get one line from each pod's log 

```shell
$ ./klogs logs --namespace kube-system --verbose apiserver --lines 2 --highlight
```

```shell
$ ./klogs audit -v -n kube-system  -ctx prod -ma 100 apiserver 
```