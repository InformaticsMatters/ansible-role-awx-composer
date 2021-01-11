Ansible Role - informaticsmatters.awx_composer
==============================================

![yamllint](https://github.com/InformaticsMatters/ansible-role-awx-composer/workflows/yamllint/badge.svg)

![GitHub release (latest by date)](https://img.shields.io/github/v/release/informaticsmatters/ansible-role-awx-composer)
![Ansible Role](https://img.shields.io/ansible/role/47735)

[![CodeFactor](https://www.codefactor.io/repository/github/informaticsmatters/ansible-role-awx-composer/badge)](https://www.codefactor.io/repository/github/informaticsmatters/ansible-role-awx-composer)

A Role to Compose (configure) an AWX server from a `tower` variable map that
you provide.

Requirements
------------

To use this role from your control machine, which runs tasks
on you control machine to interact with an AWX server using the tower-cli
and localhost, you will need: -

- `ansible` (ideally v2.9.6 or later)
- `jmespath` (ideally v0.10.0 or later)
- `ansible-tower-cli` (ideally v3.3.9 or later)
- The `awx.awx` Ansible Galaxy collection (v11.2.0 or later)

And a `tower` variable map that defines your desired AWX configuration.

Additionally, at the moment, you **MUST** provide AWS credentials (typically
allowing AWS S3 bucket access to plays that operate with S3) and Kubernetes
credentials. You will need to set the following environment variables prior
to running Ansible: -

-   `AWS_ACCESS_KEY_ID`
-   `AWS_SECRET_ACCESS_KEY`
-   `K8S_AUTH_HOST` (i.e. `https://1.2.3.4:6443`)
-   `K8S_AUTH_API_KEY` (i.e. `kubeconfig-user-xvgfv.a-abcde:0000000000000`)
-   `K8S_AUTH_VERIFY_SSL` (i.e. `no`)
    
...and in response the following custom credentials will be created on
the AWX server: -

-   `aws (SELF)`
-   `k8s (SELF)`

>   If you do not want the `aws (SELF)` credential do not define
    `AWS_ACCESS_KEY_ID`. If you do not want the `k8s (SELF)` credential
    do not define `K8S_AUTH_HOST`.

Role Variables
--------------

The role is controlled the `tower` variable, a map of material to be loaded: -

    tower:
      host: <string> (e.g. 'https://awx.example.com')
      admin_username: <string>
      admin_password: <string>
      organisation: <string>
      teams: [<string>]
      labels: [<string>]
      inventories: [<Inventory>]
      notifications: [<Notification>]
      users: [<User>]
      credentials: [<Credential>]
      projects: [<Project>]
      job_templates: [<JobTemplate>]
    
Where **Inventory** is: -

    name: <string>
    hosts: [<Host>]
    
...and **Host** is: -

    name: <string>
    groups: [<string>]    

...and **Notification** is: -

    name:
    kind:
    <kind-specific fields>

...and **User** is: -

    first_name: <string>
    last_name: <string>
    username: <string>
    password: <string>
    email: <string>
    superuser: <bool>
    teams: [<string>]
 
...and **Credential** is: -

    name:
    kind:
    <kind-specific fields>

...and **Project** is: -

    name: <string>
    description: <string>
    scm_type: <string>
    scm_url: <string>
    scm_branch: <string>
    teams: [<string>]

And **JobTemplate** is: -

    name: <string>
    project: <string>
    playbook: <string>
    ask_extra_vars: <bool>
    extra_vars: <string>
    credentials: [<string>]
    inventory: [<string>]
    teams: [<string>]
    labels: [<string>]

Dependencies
------------

You will need: -

-   `ansible`
-   `jmespath`
-   `ansible-tower-cli`
-   The `awx.awx` Ansible Galaxy collection

Example Playbook
----------------

You don't need a playbook, you just need a set of parameters - a configuration
(i.e. a `tower` map in a YAML file). If your configuration is defined in
`config.yaml` then you can configure your AWX server with the following
command: -

    $ pip install -r requirements.txt
    $ ansible-galaxy collection install -r requirements.yaml
    
    $ ansible localhost \
        -m include_role -a name=informaticsmatters.awx_composer \
        -e @config.yaml

License
-------

Apache 2.0 License

Author Information
------------------

alanbchristie
