Kitchen Example
===============

An example of using
[`rackbox`](https://github.com/teohm/rackbox-cookbook) &
[`databox`](https://github.com/teohm/databox-cookbook) and `knife-solo` to provision
a full-stack, rack-based web server.

### How generate `kitchen-example` in 4 steps:

 1. Create `Gemfile`:

    ```
    source "https://rubygems.org"
    
    gem "knife-solo", "0.3.0pre3"
    gem "berkshelf"
    ```
 2. Create `Berksfile`:

    ```
    site :opscode
    
    cookbook "runit", "1.1.2"
    cookbook "databox"
    cookbook "rackbox"
    ```
 3. Install ruby gems

    ```
    bundle install
    ```
 4. Copy the node config example

    ```
    curl https://raw.github.com/teohm/kitchen-example/master/nodes/host.json.example --output myhost.json
    ```

Provision rack-based server
-----

```
git clone git://github.com/teohm/kitchen-example.git
cd kitchen-example

# install berkshelf, knife-solo
bundle install

# download cookbooks
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

