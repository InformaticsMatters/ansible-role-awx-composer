# Role example
With an AWX server available you can run the actions from the command-line
by providing a tower map variable via a file: -

    $ ansible localhost \
        -m include_role -a name=informaticsmatters.awx_composer \
        -e "@config.yaml"

---
