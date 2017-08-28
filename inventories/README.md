Inventories
-----------

Ansible offers the possibility to use multiple inventories in order to apply different actions depending on the environment.

In this example, the development and the production environment are separated. This is useful to apply different roles, or  (in this case), to apply the same roles with different variables.


Note that the files "cross_vars" and "secrets_cross_vars" are present in both environments using a symbolic link
