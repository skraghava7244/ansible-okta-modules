# ansible-okta-modules
Ansible modules for the Okta API

### Modules

There are currently 3 modules with the following actions:

* okta_users
  * create
  * update
  * delete
  * list
  * activate
  * deactivate
* okta_groups
  * create
  * delete
  * list
  * add_user
  * remove_user
* okta_apps_swa
  * create
  * delete
  * list
  * activate
  * deactivate
  * assign_user
  * remove_user
  * assign_group
  * remove_group

### Examples

More examples can be found in `main.yml`.

#### Create User

```
- name: Create Okta user
  okta_users:
    action: create
    organization: "{{ organization }}"
    api_key: "{{ api_key }}"
    login: "{{ email }}"
    first_name: "First"
    last_name: "Last"
    activate: true
    password: "{{ password }}"
    group_ids:
      - "{{ okta_group.json.id }}"
    email: "{{ email }}"
  register: okta_user

- name: Print user information
  debug:
    msg: "{{ okta_user.json }}"
```

#### Create Group

```
- name: Create Okta group
  okta_groups:
    action: "create"
    name: "Test"
    description: ""
    organization: "{{ organization }}"
    api_key: "{{ api_key }}"
  register: okta_group

- name: Print group information
  debug:
    msg: "{{ okta_group.json }}"
```

#### Create custom SWA app

```
- name: Create Okta app
  okta_apps_swa:
    action: create
    label: "Ansible Test"
    organization: "{{ organization }}"
    api_key: "{{ api_key }}"
    login_url: "https://unicorns.lol/login"
    redirect_url: "https://unicorns.lol/redirect"
  register: okta_app

- name: Print app information
  debug:
    msg: "{{ okta_app.json }}"
```
