# imageio-ansible
There are two ways to run ansible playbooks on TVM to configure imageio

1. Providing username and password of respective proxy and daemon hosts in inventory file.
   Example:
    * For daemon, update imageio-ansible/inventories/production/daemon file with following contents.
    [hosts]
    <host ip> ansible_user=<user_name> ansible_ssh_pass=<password>
    * For proxy, update imageio-ansible/inventories/production/proxy file with following contents.
    [hosts]
    <manager ip> ansible_user=<user_name> ansible_ssh_pass=<password>
    * To run ansible playbook from TVM on daemon/proxy hosts, refer below example.
    ansible-playbook site.yml -i inventories/production/daemon --tags “daemon”

2. Passwordless login to proxy and daemon hosts
    * Check if TVM has private and public keys generated at path ~/.ssh/
    * If yes,
    Then copy public key and add it in ~/.ssh/authorized_keys file of daemon/proxy hosts on which you want to run scripts.
    * If no,
    Generate keys on TVM using ssh-keygen command, and pass appropriate passphrase to generate the keys.
    Then copy public key and add it in ~/.ssh/authorized_keys file of daemon/proxy hosts on which you want to run scripts.
    * While running ansible playbook from TVM on daemon/proxy hosts, pass private key file of TVM to ansible-playbook command.
    Example: ansible-playbook test.yml -i inventories/hosts --private-key ~/.ssh/id_rsa --tags “daemon”
