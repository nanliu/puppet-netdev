# OVERVIEW

Puppet module that provides vendor agnostic resource-types for networking device abstractions.

# EXAMPLE USAGE

This module has been tested against Puppet agent 2.7.19.  Here is a short example of a static manifest for a Junos EX switch.  This example assumes that you've also installed the Puppet _stdlib_ module as this example uses the _keys_ function.

~~~~
node "myswitch1234.mycorp.com" {
     
  netdev_device { $hostname: }
    
  $vlans = {
    'Blue'    => { vlan_id => 100, description => "This is a Blue vlan" },
    'Green'   => { vlan_id => 101, description => "This is a Green vLAN" },
    'Purple'  => { vlan_id => 102, description => "This is a Puple vlan" },
    'Red'     => { vlan_id => 103, description => "This is a Red vlan" },
    'Yellow'  => { vlan_id => 104, description => "This is a Yellow vlan" }   
  }
    
  create_resources( netdev_vlan, $vlans )
    
  $access_ports = [
    'ge-0/0/0',
    'ge-0/0/1',
    'ge-0/0/2'
  ]
    
  $uplink_ports = [
    'xe-0/0/0',
    'xe-0/0/2'
  ]
      
  netdev_l2_interface { $access_ports:
    untagged_vlan => Blue
  }
          
  netdev_l2_interface { $uplink_ports:
    tagged_vlans => keys( $vlans )
  }
}
~~~~
  
# DEPENDENCIES

  * Puppet 2.7.19
  * Ruby Gem netconf 0.2.5

# INSTALLATION ON PUPPET-MASTER

  * gem install netconf
  * puppet module install jeremyschulman-netdev 

# RESOURCE TYPES

See RESOURCE-TYPES.md for documentation and usage examples

# LICENSE

See LICENSE.md
