Kitchen Example
===============

An example of using rackbox & databox and chef-solo to provision
a full-stack rack-based web server.

Usage
-----

```
bundle install

# vendoring cookbooks
bundle exec berks install -p cookbooks/

# copy & edit the node config
cp nodes/host.json.example prod_host1.json

# setup chef-solo on the node
bundle exec knife solo prepare prod_host1

# provision the node
bundle exec knife solo cook prod_host1
```
