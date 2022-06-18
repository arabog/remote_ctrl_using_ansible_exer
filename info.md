# # Example inventory that makes an alias for localhost that uses Python3
# localhost-py3 ansible_host=localhost ansible_connection=local ansible_python_interpreter=/usr/bin/python3

# # Example of setting a group of hosts to use Python3
# [py3-hosts]
# ubuntu20
# # fedora27

# [py3-hosts:vars]
# ansible_python_interpreter=/usr/bin/python334.203.203.133


# [WARNING]: provided hosts list is empty, only localhost is available. Note that
# the implicit localhost does not match 'all'

# https://docs.ansible.com/ansible/latest/reference_appendices/python_3_support.html#:~:text=Ansible%20will%20automatically%20detect%20and,%2Fusr%2Fbin%2Fpython3.

# ansible-playbook main-remote.yml -i inventory --private-key ansible.pem -e 'ansible_python_interpreter=/usr/bin/python3'
