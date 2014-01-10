# OpenShift ElasticSearch Cartridge

Running scalable ElasticSearch on OpenShift.

The first gear is the master and data node. All other gears will play the data-only
node role. In order to create data-only nodes, simply scale-up your app.

## Usage

First of all, create your account on Getup Cloud: http://getupcloud.com.
It is free and gives a 750h trial period.

Let's start by creating a new ES app called `elastic`:

```
$ rhc app create -s elastic https://reflector-getupcloud.getup.io/reflect?github=caruccio/openshift-elasticsearch
$ cd elastic
```

Point your browser to [http://elastic-$namespace.getup.io](http://elastic-$namespace.getup.io) to see it in action.
You can contemplate your "cluster" in [http://elastic-$namespace.getup.io/_cluster/nodes/stats?plugins=true](http://elastic-$namespace.getup.io/_cluster/nodes/stats?plugins=true).
_(Look mom! I've built a cluster of a single node!)_

To add 4 more data-only ES instances, simply add more gears:

```
$ rhc cartridge-scale elasticsearch 4 -a elastic
```

Now you can be proud and show off with your amazing pile of pure distributed-real-time-analytics-multi-tenant-document-oriented-restful-schema-free-per-operation-persistent-open-source-o-matic server.

## Plugins

The app is created with 3 installed plugins by default:

* [mobz/elasticsearch-head](http://mobz.github.io/elasticsearch-head)
* [karmi/elasticsearch-paramedic](https://github.com/karmi/elasticsearch-paramedic)
* [polyfractal/elasticsearch-inquisitor](https://github.com/polyfractal/elasticsearch-inquisitor)

In order to install/remove plugins, edit file `plugins.txt`, commit and push.
If your plugin needs a full URL to download its code from, use `NAME=URL` to specify it.
All plugins are installed on all gears.

## Contributions

Please, anything...

Here are some suggestions:

* Download and install elasticsearch source on-the-fly
* User can choose what version it wants to run
* Better (?) cluster topology
