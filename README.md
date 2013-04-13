Kitchen Example
===============

An example of using rackbox & databox and chef-solo to provision
a full-stack rack-based web server.

Provision a full-stack, rack-based server
-----

```
bundle install

# vendoring cookbooks
bundle exec berks install -p cookbooks/

# copy & edit the node config
cp nodes/host.json.example testbox.json

# setup chef-solo on the node
bundle exec knife solo prepare testbox

# provision the node
bundle exec knife solo cook testbox
```

Deploy rails on unicorn
-------------
```
git clone git://github.com/teohm/sample-app1.git
cd sample-app1
bundle install
ssh testbox 
#
# in testbox, add SSH known host by running:
#    ssh git@github.com   
#
bundle exec cap deploy:setup
bundle exec cap deploy:migrations
```

Deploy rails on passenger
-------------
```
git clone git://github.com/teohm/sample-app2.git
cd sample-app2
bundle install
ssh testbox 
#
# in testbox, add SSH known host by running:
#    ssh git@github.com   
#
bundle exec cap deploy:setup
bundle exec cap deploy:migrations
```

