Ansible Role - informaticsmatters.awx_composer
==============================================

A Role to Compose (configure) an AWX server from a `tower` variable map that
you provide.

Requirements
------------

To use this role from your control machine, which runs tasks
on you control machine to interact with an AWX server using the tower-cli
and localhost, you will need: -

- `ansible` (ideally v2.9.6 or later)
- The `awx.awx` Ansible Galaxy collection
- `tower-cli` (ideally v3.3.9 or later)
- A `tower` variable map that defines your required configuration

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
      users: [<User>]
      credentials: [<Credential>]
      projects: [<Project>]
      job_templates: [<JobTemplate]
    
Where **User** is: -

    first_name: <string>
    last_name: <string>
    username: <string>
    password: <string>
    email: <string>
    superuser: <bool>
    teams: [<string>]
 
And **Credential** is: -

    name:
    kind:
    <credential-specific fields>

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
    teams: [<string>]
    labels: [<string>]

Dependencies
------------

You will need: -

-   `ansible`
-   `tower-cli`

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
        -e "@config.yaml"

License
-------

Apache 2.0 License

Author Information
------------------

alanbchristie
