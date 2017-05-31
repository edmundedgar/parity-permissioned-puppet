This sets up nodes in a parity private network, running in systemd. It is intended for our particular application and will need to be customized or generalized to use on anything else. The name of the network is hard-coded, as are various other parameters including validator addresses.

To set up a node, we run
sudo ./setup.sh [noparity]

It assumes you have generated the validator keys on other systems, and copied them over manually. (See error message when you run setup.sh without doing this)

The following are hard-coded:

 * modules/parity/manifests/init.pp: 
   The signing accounts of the validator accounts, and a single deployer account. These are used to generate the genesis file.

 * modules/parity/files/reserved-peers.txt:
   The enodes and IP addresses of the permitted peers. On a new install the network will not sync until these are updated.
   The enode of each node is output by the setup script, which gets it from syslog.

The setup includes a non-validator node for running truffle deployments and other command-line scripts.
The truffle installation is not in puppet, although puppet handles some dependencies. 
Run truffle-setup.sh after running setup.sh.

We also do not automate copying over the truffle build directory to the static web server, which you can do with rsync.
