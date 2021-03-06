# 1603470643 puppet-master-defining-catalog-for-agents
The master contains a `site.pp` file. This file will contain how to configure all of the agents or specific agents. This file should be found here:
```
/etc/puppetlabs/code/environments/production/manifests/site.pp
```

Below is an example of the contents of the site.pp
```ruby
# This will be applied to all agents
file {'AgentTestfileALL.txt':
    ensure  => present,
    path    => '/tmp/AgentTestfileALL.txt',
    mode    => '0777',
    content => "Hello ALL agents \n",
}

node '9e50cf884c7d' {
        file {'AgentTestfile1.txt':
            ensure  => present,
                path    => '/tmp/AgentTestfile1.txt',
                mode    => '0777',
                content => "Hello agent 9e50cf884c7d \n",
        }
}
```

As you can se the first file called `AgentTestfileAll.txt` will be applied to every agent.
However the `AgentTestfile1.txt` will only be applied to the puppet agent whos hostname is `9e50cf884c7d`


The puppet master will compile the above `site.pp` into a catalog for each node. 
When the puppet agent then tries to apply these configurations this catalog will be downloaded from the master and cached on the puppet agent locally.
This is so if network connectivity to the master was an issue that state can still be applied to the VM/puppet agent.

[Where is this catalog cached and what it looks like?](1603470422-puppet-agent-catalog-cache.md)


## Links
- [1603470422-puppet-agent-catalog-cache.md](1603470422-puppet-agent-catalog-cache.md)
- [1603473949-puppet-master-functions.md](1603473949-puppet-master-functions.md)
- [1603725828-puppet-dual-api-key-implementation.md](1603725828-puppet-dual-api-key-implementation.md)
