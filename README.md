# Pool Recycle plugin for tsuru

This plugin allows tsuru to recreate one entire pool based on IaaS templates associate with it.

## Dependencies
You will need just admin permission in tsuru.

## Installing

As easy as any other tsuru plugin (use the same command to upgrade)
```bash
$ tsuru plugin-install admtools https://raw.githubusercontent.com/tsuru/pool_recycle/master/pool_recycle/plugin.py
$ tsuru pool_recycle -h 
usage: pool_recycle [-h] -p POOL [-r DESTROY_NODE] [-d] [-P DOCKER_PORT]
                    [-s DOCKER_SCHEME]

Tsuru pool nodes recycle

optional arguments:
  -h, --help            show this help message and exit
  -p POOL, --pool POOL  Docker tsuru pool
  -r DESTROY_NODE, --destroy-node DESTROY_NODE
                        Destroy olds docker nodes after recycle
  -d, --dry-run         Dry run all recycle actions
  -P DOCKER_PORT, --docker-port DOCKER_PORT
                        Docker port - if something goes wrong, node will be
                        re-add using it as docker port (only when using IaaS)
  -s DOCKER_SCHEME, --docker-scheme DOCKER_SCHEME
                        Docker scheme - if something goes wrong, node will be
                        re-add using it as docker scheme (only when using
                        IaaS)
```

## Example (running with dry mode)

```bash
$ tsuru pool_recycle -p theonepool -d
Creating new node on pool "theonepool" using "templateA" template
Removing node "http://127.0.0.1:2375" from pool "theonepool"
Moving all containers on old node "http://127.0.0.1:2375" to new node

Creating new node on pool "theonepool" using "templateB" template
Removing node "http://192.168.50.6:2375" from pool "theonepool"
Moving all containers on old node "http://192.168.50.6:2375" to new node
```
