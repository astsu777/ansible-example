# Introduction
These files are just an example of a scalable Ansible structure. This structure of inventories, roles and variables is the most flexible one you can possibly do.

Besides, this structure respects the Ansible best-practices.


# Structure

Here is the file structure you can find:

```
- inventories: this folder contains the different environment you can have (development, staging, production, etc...)
- roles: this folder contains all the roles that are applicable for the environments
- ansible.cfg: this file overrides the default Ansible configuration with certain custom values
- site.yml: this is the main playbook file
- common.yml: this playbook contains common roles that can be safely applied to all hosts
- database.yml: this playbook contains tasks used only for database servers
- webserver.yml: this playbook contains tasks used only for Web servers
```

If you take a look at the [Ansible best practices](http://docs.ansible.com/ansible/latest/playbooks_best_practices.html#alternative-directory-layout), you will see that other folders can also be present if necessary.


# Resources

Here are some useful resources you might want to check:

- [Ansible Best Practices](http://docs.ansible.com/ansible/latest/playbooks_best_practices.html): useful to always respect the best practices
- [Ansible Variables Precedence Order](http://docs.ansible.com/ansible/latest/playbooks_variables.html#variable-precedence-where-should-i-put-a-variable): there is an order or priority in which the variables are read. It is good to know this before you define your variables.
- [Ansible Galaxy](https://galaxy.ansible.com/): good resource to find a lot of playbook and roles example
