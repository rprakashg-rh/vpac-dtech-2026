#cms
This section shows how to apply some of the day 2 configs to AAP controller from git using gitops methodologies


```sh
ansible-playbook --vault-password-file <(echo "$VAULT_SECRET") configure_aap.yml -e environment=demo
```