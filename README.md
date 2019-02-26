# nginx-proxy setup

See https://gitlab.com/rickselby-linode-setup/main/wikis/home for initial details

## networks.sh

I've found it best to create the neworks outside of the individual docker-compose files,
so the nginx-proxy container can be added to the networks once, not every time the stack is reloaded.
It also allows closer control over the networks created - these are much smaller - /16 is not needed for a single website!
(Honestly, /24 is overkill too, but it keeps the IP addresses simple.)

To achieve this, there's `networks.sh`. 
Add each new network to the array at the top and commit; the CI will setup the new network.

Do not re-order the networks once they're created - the script is assigning subnets
sequentially, and re-ordering the networks could break things.
