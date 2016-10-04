In this tutorial we are going to perform exactly the same tasks we did on the previous tutorial. However, this time we will use napalm.

Requirements
------------

    pip install -r requirements.txt

inv site.create -n acme -d "Acme Corp."
inv site.add_atribbutes -s acme -f data/acme/attributes.yml
inv site.add_devices -s acme -f data/acme/devices.yml
inv serivce.loopbacks -s acme -f data/acme/services.yml
inv serivce.ipfabric -s acme -f data/acme/services.yml


ansible-playbook playbook_configure.yml -l acme
ansible-playbook playbook_configure.yml -l acme -e commit_changes=1

# Uncomment data/services.yml
inv site.create -n evil -d "Evil Corp."
inv site.add_atribbutes -s evil -f data/evil/attributes.yml
inv site.add_devices -s evil -f data/evil/devices.yml
inv serivce.loopbacks -s evil -f data/evil/services.yml
inv serivce.ipfabric -s evil -f data/evil/services.yml

ansible-playbook playbook_configure.yml -l evil
ansible-playbook playbook_configure.yml -l evil -e commit_changes=1


# Change networks and deploy new site
inv site.create -n evil -d "My evil site"