# Dockerized Odoo

This is a flexible and **streamlined** version of most dockerized Odoo projects that you'll find. And one that allows you to deploy with two different methods using the same Dockerfile:

* **Standalone**: As most people use their implementation. With Odoo's source code inside the container. **This is the default**
* **Hosted**: A more practical deployment for **development**, as the HOST (where docker is installed) has the source code, and each container uses this single source.

Dockerdoo is integrated with **VSCode** for fast development and debugging, just install the [Remote Containers extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers).

> By default this approach does not use the modules availables at the `./custom` directory, as this uses Docker's hosted volumes approach which is considerably slow on Mac and PC. If you'd like to use it this way, just uncomment `./custom:${ODOO_EXTRA_ADDONS}:delegated` from the `dev-vscode.yml`

## Quick usage

To use the **hosted** approach, the Odoo code must be in the `./src` directory, if you also use Enterprise you can add it to the `custom` directory, which is automagically added to your addons_path.

### Project Structure

```bash
your-project/
 ├── resources/         # Scripts for service automation
 ├── src/
 │   └── odoo/          # Just required if using hosted source code
 │
 ├── config/
 │   └── odoo.conf      # Hosted configuration file for hosted environment
 ├── custom/            # Custom modules goes here, same level hierarchy **REQUIRED**
 │   ├── custom/
 │   ├── OCA/
 │   ├── enterprise/
 │   └── /
 ├── ...                # Common files (.gitignore, etc.)
 ├── .env               # Single source of environment definition
 ├── Dockerfile         # Single source of image definition
 ├── docker-compose.yml             # The opionated version
 └── docker-compose.override.yml    # Your custom version
```

### Extra addons

You can put all your **custom addons** in the folder `./custom/`, those will be automatically added to your `addons_path` thanks to the script in `./resources/getaddons.py`

## Credits

Mainly based on dockery-odoo work by:

* [David Arnold](https://github.com/blaggacao) ([XOE Solutions](https://xoe.solutions))

Bunch of ideas taken from:

* [Odoo](https://github.com/odoo) ([docker](https://github.com/odoo/docker))
* [OCA](https://github.com/OCA) ([maintainer-quality-tools](https://github.com/OCA/maintainer-quality-tools))
* [Ingeniería ADHOC](https://github.com/jjscarafia) ([docker-odoo-adhoc](https://github.com/ingadhoc/docker-odoo-adhoc))

## WIP

* Swarm / Kubernetes considerations (secrets, etc.)
