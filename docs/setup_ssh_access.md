# setup_ssh_access
This section walks through setps to setup SSH access to RHEL hosts

1) First create a new ssh key by running command below
2) 
   ```sh
   ssh-keygen -t rsa -b 4096 -C "<replace>"
   ```

   Then we create an `.ssh` directory under the current ansible user's home and add the public key of newly generated SSH key to authorized keys.

   All these steps are automated in a simple ansible playbook that we can execute on the control machine as shown below

   ```sh
   ansible-playbook -i inventory setup_ssh_access.yml
   ```
   
