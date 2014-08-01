Get OpenStack Credentials
------
* Get an openstack user name and password. Talk to IT.

* Once you get creds copy over keystone_auth-dist to keystone_auth and enter in your credentials

* Make sure you can loggin to keystone.

* Install and activate a python virtualenv

* Install OpenStack CLIs
::
    pip install -r requirements.txt

* Upload you SSH key
::
    nova keypair-add --pub-key ~/.ssh/id_rsa.pub $(whoami)-key

* Down load a heat template
::
    wget https://raw.githubusercontent.com/uberj/dpaste/master/dpaste-new-neutron-env.yaml

* Figure out the UUID of the public network
::
    neutron net-show public | grep ' id ' | awk '{print $3}'

* Tell OpenStack to create a stack
::
    heat stack-create dpaste -r --template-file=dpaste-new-neutron-env.yaml --parameters="key_name=$(whoami)-key;public_net_id=<public-network_uuid>"

* Wait for your stack to be created
::
    watch -n 0.5 heat stack-list
