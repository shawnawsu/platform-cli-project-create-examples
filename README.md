[![Try on Platform.sh](https://console.platform.sh/projects/create-project?template=sometemplateurihere)](https://platform.sh)

# platform-cli-project-create-examples

The example files contained here work with the `project:create` command and its options. The **Platform.sh CLI** is the official command-line interface for [Platform.sh](https://platform.sh) more information, including installation instructions can be found here: https://github.com/platformsh/platformsh-cli.

## Project:create

```Command: project:create
Aliases: create
Description: Create a new project

Usage:
 platform create [--title TITLE] [--catalog_url CATALOG_URL] [--region REGION] [--plan PLAN] [--environments ENVIRONMENTS] [--storage STORAGE] [--initialized INITIALIZED] [--check-timeout CHECK-TIMEOUT] [--timeout TIMEOUT] [--template TEMPLATE] [--catalog] [--initialize] [--current-repo]

Options:
      --title=TITLE                  The initial project title
                                     [default: "Untitled Project"]
      
      --catalog_url=CATALOG_URL      The template from which to create your
                                     project or your own blank project.
      
      --region=REGION                The region where the project will be
                                     hosted ('eu-2.platform.sh',
                                     'us-2.platform.sh', 'au.platform.sh',
                                     'ca-1.platform.sh')
     
      --plan=PLAN                    The subscription plan (e.g. 'development',
                                     'standard', 'medium', 'large')
                                     [default: "development"]
     
      --environments=ENVIRONMENTS    The number of environments
                                     [default: 3]
     
      --storage=STORAGE              The amount of storage per environment, in
                                     GiB [default: 5]
     
      --initialized=INITIALIZED      Initialize this environment?
                                     [default: true]
     
      --check-timeout=CHECK-TIMEOUT  The API timeout while checking the project
                                     status [default: 30]
     
      --timeout=TIMEOUT              The total timeout for all API checks (0 to
                                     disable the timeout) [default:
                                     900]
     
      --template=TEMPLATE            Choose a starting template or provide a
                                     url of one.
     
      --catalog                      An option that adds additional form fields 
                                     which allow for the choice a template from 
                                     the catalog
      
      --initialize                   An option that will automatically initialize
                                     the project and skip the form field. 

      --current-repo                 Automatically set-remote after project
                                     creation.
  
  -h, --help                         Display this help message
  
  -q, --quiet                        Do not output any message
  
  -V, --version                      Display this application version
  
  -y, --yes                          Answer "yes" to all prompts; disable
                                     interaction
  
  -n, --no                           Answer "no" to all prompts
  
  -v|vv|vvv, --verbose               Increase the verbosity of messages

Help:
 Use this command to create a new project.
 
 An interactive form will be presented with the available options. But if the
 command is run non-interactively (with --yes), the form will not be displayed,
 and the --region option will be required.
 
 A project subscription will be requested, and then checked periodically (every 3
 seconds) until the project has been activated, or until the process times out
 (after 15 minutes by default).
 
 If known, the project ID will be output to STDOUT. All other output will be sent
 to STDERR.
```

## Catalog

A catalog is a list of template objects. Template objects are composed of an `info` and a `template` key. The info key is used to render the template for selection:

```
info:
    description: WordPress is the world's most widely used lightweight CMS and blogging
      tool.
    id: platformsh/wordpress
    image: data:image/svg+xml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0idXRmLTgiPz4KPCEtLSBHZW5lcmF0b3I6IEFkb2JlIElsbHVzdHJhdG9yIDIzLjAuMSwgU1ZHIEV4cG9ydCBQbHVnLUluIC4gU1ZHIFZlcnNpb246IDYuMDAgQnVpbGQgMCkgIC0tPgo8c3ZnIHZlcnNpb249IjEuMSIgaWQ9IkxheWVyXzEiIHhtbG5zOnJkZj0iaHR0cDovL3d3dy53My5vcmcvMTk5OS8wMi8yMi1yZGYtc3ludGF4LW5zIyIKCSB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB4PSIwcHgiIHk9IjBweCIgdmlld0JveD0iMCAwIDQwIDQwIgoJIHN0eWxlPSJlbmFibGUtYmFja2dyb3VuZDpuZXcgMCAwIDQwIDQwOyIgeG1sOnNwYWNlPSJwcmVzZXJ2ZSI+CjxzdHlsZSB0eXBlPSJ0ZXh0L2NzcyI+Cgkuc3Qwe2ZpbGwtcnVsZTpldmVub2RkO2NsaXAtcnVsZTpldmVub2RkO2ZpbGw6IzQ2NDM0Mjt9Cjwvc3R5bGU+CjxnIHRyYW5zZm9ybT0ibWF0cml4KDEuMDc1NSAwIDAgMS4wNzU1IC0zLjUxMDMgLTEuNjY4NCkiPgoJPHBhdGggY2xhc3M9InN0MCIgZD0iTTIxLjksMy4xYzQuNCwwLDguNSwxLjcsMTEuNSw0LjVjLTEuNSwwLTMsMC44LTMsMi45Yy0wLjEsNC4xLDQuOSw1LDIuMiwxMy4ybC0yLjIsNi44bC02LjEtMTcuOQoJCWMtMC4xLTAuMywwLTAuNCwwLjQtMC40aDEuN2MwLjEsMCwwLjItMC4xLDAuMi0wLjJ2LTFjMC0wLjEtMC4xLTAuMi0wLjItMC4yYy0zLjMsMC4xLTYuNSwwLjEtOS43LDBjLTAuMSwwLTAuMiwwLjEtMC4yLDAuMnYxCgkJYzAsMC4xLDAuMSwwLjIsMC4yLDAuMmgxLjdjMC40LDAsMC41LDAuMSwwLjYsMC40bDIuNSw2LjhsLTMuOCwxMS4zbC02LjItMTguMmMtMC4xLTAuMiwwLTAuNCwwLjItMC40aDJjMC4xLDAsMC4yLTAuMSwwLjItMC4ydi0xCgkJYzAtMC4xLTAuMS0wLjItMC4yLTAuMmMtMi4xLDAuMS00LjEsMC4xLTYuMSwwLjJDMTAuNiw2LjIsMTUuOSwzLjEsMjEuOSwzLjFMMjEuOSwzLjFMMjEuOSwzLjF6IE0zNi44LDEyLjFjMS4zLDIuNCwyLDUuMiwyLDguMQoJCWMwLDYuNC0zLjYsMTItOC44LDE0LjlsNS4zLTE1QzM2LjEsMTcuNywzNi45LDE0LjYsMzYuOCwxMi4xTDM2LjgsMTIuMUwzNi44LDEyLjF6IE0yNy42LDM2LjJjLTEuOCwwLjYtMy43LDEtNS43LDEKCQljLTEuNywwLTMuNC0wLjMtNC45LTAuN2w1LjItMTVMMjcuNiwzNi4yTDI3LjYsMzYuMkwyNy42LDM2LjJ6IE0xNC42LDM1LjVjLTUuNy0yLjctOS43LTguNi05LjctMTUuNGMwLTIuNSwwLjUtNC45LDEuNS03LjEKCQlMMTQuNiwzNS41TDE0LjYsMzUuNUwxNC42LDM1LjV6IE0yMS45LDEuNmMxMC4zLDAsMTguNiw4LjMsMTguNiwxOC42cy04LjMsMTguNi0xOC42LDE4LjZTMy4zLDMwLjQsMy4zLDIwLjFTMTEuNiwxLjYsMjEuOSwxLjZ6IgoJCS8+CjwvZz4KPC9zdmc+Cg==
    name: Wordpress
    notes:
    - content: PHP 7.2<br/>MySQL 10.2
      heading: Apps & Services
    tags:
    - PHP
    - WordPress
    - CMS
template: https://github.com/platformsh/template-builder/blob/master/templates/wordpress/files/.platform.template.yaml
```
### Info Key
The info key contains the `title`, a list of content blocks for rendering in the template description, and a set of tags used to present a filtering interface. 

### Template Key
The template key is the URL to the actual template _file_, which is a different format of file described below. 


## Template Files

A template file contains a list of keys that Platform.sh uses during the initial settings and creation process of a project. The contents of the template file controls the project's intital setup behavior and sets restrictions on the resources a given project can consume. 

```
info:
  # Unique machine name, prefaced by a vendor or organization identifier
  id: platformsh/drupal7

  # The human-readable name of the template.
  name: Drupal 7

  # Human-readable descriptive text for the template. Supports limited HTML.
  description: |
    <p>This template builds a Drupal 7 site using Drush make.</p>
    <p>Drupal is a flexible and extensible PHP-based CMS framework.  Version 7 is the legacy support version.</p>

  # A list of tags associated with the template.
  tags:
  - PHP
  - Drupal
  - CMS

  # An image URI (either base64-encoded or a URL) representing the template.
  image: data:image/svg+xml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0idXRmLTgiPz4KPCEtLSBHZW5lcmF0b3I6IEFkb2JlIElsbHVzdHJhdG9yIDIzLjAuMSwgU1ZHIEV4cG9ydCBQbHVnLUluIC4gU1ZHIFZlcnNpb246IDYuMDAgQnVpbGQgMCkgIC0tPgo8c3ZnIHZlcnNpb249IjEuMSIgaWQ9IkxheWVyXzEiIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyIgeG1sbnM6eGxpbms9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGxpbmsiIHg9IjBweCIgeT0iMHB4IgoJIHZpZXdCb3g9IjAgMCAzNSA0MCIgc3R5bGU9ImVuYWJsZS1iYWNrZ3JvdW5kOm5ldyAwIDAgMzUgNDA7IiB4bWw6c3BhY2U9InByZXNlcnZlIj4KPHN0eWxlIHR5cGU9InRleHQvY3NzIj4KCS5zdDB7ZmlsbC1ydWxlOmV2ZW5vZGQ7Y2xpcC1ydWxlOmV2ZW5vZGQ7ZmlsbDojMDA4RUNFO30KPC9zdHlsZT4KPGc+CjwvZz4KPHBhdGggY2xhc3M9InN0MCIgZD0iTTI0LDYuNmMwLDAtMi4zLTEtMy42LTEuOGMwLDAtMS43LTEtNC41LTQuN2MwLDAsMC4xLDQuMi00LjQsNi40QzQuNCw5LjMsMCwxNS4yLDAsMjIuN0MwLDMyLjIsNy44LDQwLDE3LjMsNDAKCWM5LjYsMCwxNy4zLTcuOCwxNy4zLTE3LjNDMzQuNywxMS4xLDI0LDYuNiwyNCw2LjZ6IE00LjgsMTYuMWMtMi43LDAuNi0yLjUtMC44LTItMmMwLjItMC43LDAuOS0xLjUsMC45LTEuNWMxLjgtMi45LDUuOC01LDUuOC01CglsMCwwYzAuNS0wLjIsMS40LTAuNywyLjItMS4xYzEuNi0wLjksMi0xLjQsMi0xLjRjMi4zLTIuMiwyLjEtNC45LDIuMS01YzAsMCwwLDAsMCwwYzAsMCwwLDAsMCwwdjBjMCwwLDAsMCwwLDAKCWMyLDQtMC40LDUuOC0wLjQsNS44YzAuNiwwLjYsMC40LDEuMiwwLjQsMS4yQzEyLjcsMTMuOCw0LjgsMTYuMSw0LjgsMTYuMXogTTI1LjcsMzcuMWMtMC4yLDAuMS0yLjcsMS4zLTUuNiwxLjMKCWMtMS42LDAtMy4zLTAuNC00LjgtMS40Yy0wLjUtMC40LTAuNy0xLjEtMC40LTEuNmMwLjEtMC4yLDAuNy0wLjksMi4xLDBsMCwwYzAuMSwwLjEsMy40LDIuMyw4LjUtMC41YzAuNC0wLjIsMC45LTAuMSwxLjEsMC4zCglDMjYuOSwzNS42LDI3LDM2LjQsMjUuNywzNy4xeiBNMTguNywzMi45bDAuMS0wLjFjMC4xLTAuMSwxLjgtMi4zLDQuMy0yYzAuNCwwLDEuOCwwLjEsMi43LDEuOGMwLjEsMC4yLDAuMywwLjktMC4xLDEuNAoJYy0wLjIsMC4yLTAuNSwwLjQtMS4xLDAuMmMtMC40LTAuMS0wLjYtMC41LTAuNi0wLjdsMCwwYy0wLjEtMC4zLTAuMi0wLjUtMS4yLTAuNmMtMC44LTAuMS0xLjMsMC4zLTEuOSwwLjgKCWMtMC4zLDAuMy0wLjcsMC42LTEuMSwwLjdjLTAuMSwwLjEtMC4yLDAuMS0wLjQsMC4xYy0wLjIsMC0wLjQtMC4xLTAuNi0wLjJDMTguNSwzNCwxOC40LDMzLjYsMTguNywzMi45eiBNMzAuMSwzMy4xCgljMCwwLTAuOSwwLjMtMS44LTAuN2MwLDAtMi43LTMuMS00LTMuNmMwLDAtMC44LTAuMy0xLjgsMC4xYzAsMC0wLjcsMC4xLTMuNCwxLjljMCwwLTQuNiwyLjktNi45LDIuNWMwLDAtNS4yLDAuMS00LjUtNS40CgljMCwwLDEuMS02LjIsOC4zLTQuOGMwLDAsMS42LDAuMyw0LjUsMi42YzAsMCwyLDEuNSwzLDEuNWMwLDAsMC44LDAuMSwyLjYtMWMwLDAsMy41LTIuNyw0LjgtMi42YzAsMCwwLDAsMCwwCgljMC4yLDAsMi41LTAuMSwyLjUsMy43QzMzLjMsMjcuMiwzMy40LDMxLjYsMzAuMSwzMy4xeiIvPgo8L3N2Zz4K
  
  # Additional notes displayed in the template's detail view.
  # Each note object is displayed as a small section heading with content below. Supports limited HTML.
  notes:
    - heading: "Apps & Services"
      content: "PHP 7.2<br/>MySQL 10.2"

# This key describes the initialization call made to the master environment at
# project creation time. This is part of the full v2 UI operation mode, which
# places project schema/options selection early in the creation process, rather
# than later as it exitss now. To allow this schema to be backwards-compatible,
# this key also gets mapped to the appropriate location in project.settings so
# that the current UI can have its own workflow overridden as well.
initialize:
  repository: git://github.com/platformsh/template-drupal7.git@master
  config: null
  files: []
  profile: Drupal 7

# The default key allows the `YAML` file to make additional changes to the project after 
# it has been provisioned but before the subscrition is marked as active. 
defaults:
  # Here the `variables` key allows default project-level variables to be set. 
  variables:
    - name: env:COMPOSER_AUTH
      value: ""
      is_json: false
      visible_build: true
      visible_runtime: false
    - name: drupal7:site_name
      value: "Hello, world!"
      is_json: false
      visible_build: false
      visible_runtime: true

  # A list of UUIDs and access levels for the project
  access:
    - user: [UUID HERE]
      role: admin
    - user: [UUID HERE]
      role: viewer
    - email: [EMAIL HERE]
      role: admin
    - user: [UUID HERE]

#This key allows the list of available regions to be expanded or restricted for a particular project.
regions:
  # This adds regions not in the default list, making them
  # accessible to the user for this project/checkout.
  additional:
    - bc.platform.sh
  # This key overrides the list provided by the defaults + the additional key,
  # but does not permit access to any excluded regions. For this key, the last
  # implementation of this key will "win".
  only:
    - us.platform.sh
    - eu.platform.sh
      # Removes regions from the list and blocks them from being used for
  # this project.
  exclude: 
    - us-2.platform.sh
    - au.platform.sh
    - eu-2.platform.sh
    - nl-1.platform.sh

## Sets the available plans in the same way:
plans:
  # Removes plans from the list and bloceks them from being used for this
  # project.
  exclude:
    - development
    - small
  # This adds regions not in the default list, making them
  # accessible to the user for this project/checkout.    
  additional:
    - 2xlarge
    - xlarge
  # This key overrides the list provided by the defaults + the additional key,
  # but does not permit access to any excluded plans. For this key, the last
  # implementation of this key will "win" (i.e. the project level will supersede
  # the vendor level if this key is present.)
  only:
    - development
    - standard
    - medium
    - large

```

### Template file: info

This should match the `info` key present in the catalog item. This isn't required, but it's helpful to think of the catalog as being constructed by taking the `info` key out of each template file.

```
info:
  # Unique machine name, prefaced by a vendor or organization identifier
  id: platformsh/drupal7

  # The human-readable name of the template.
  name: Drupal 7

  # Human-readable descriptive text for the template. Supports limited HTML.
  description: |
    <p>This template builds a Drupal 7 site using Drush make.</p>
    <p>Drupal is a flexible and extensible PHP-based CMS framework.  Version 7 is the legacy support version.</p>

  # A list of tags associated with the template.
  tags:
  - PHP
  - Drupal
  - CMS

  # An image URI (either base64-encoded or a URL) representing the template.
  image: data:image/svg+xml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0idXRmLTgiPz4KPCEtLSBHZW5lcmF0b3I6IEFkb2JlIElsbHVzdHJhdG9yIDIzLjAuMSwgU1ZHIEV4cG9ydCBQbHVnLUluIC4gU1ZHIFZlcnNpb246IDYuMDAgQnVpbGQgMCkgIC0tPgo8c3ZnIHZlcnNpb249IjEuMSIgaWQ9IkxheWVyXzEiIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyIgeG1sbnM6eGxpbms9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGxpbmsiIHg9IjBweCIgeT0iMHB4IgoJIHZpZXdCb3g9IjAgMCAzNSA0MCIgc3R5bGU9ImVuYWJsZS1iYWNrZ3JvdW5kOm5ldyAwIDAgMzUgNDA7IiB4bWw6c3BhY2U9InByZXNlcnZlIj4KPHN0eWxlIHR5cGU9InRleHQvY3NzIj4KCS5zdDB7ZmlsbC1ydWxlOmV2ZW5vZGQ7Y2xpcC1ydWxlOmV2ZW5vZGQ7ZmlsbDojMDA4RUNFO30KPC9zdHlsZT4KPGc+CjwvZz4KPHBhdGggY2xhc3M9InN0MCIgZD0iTTI0LDYuNmMwLDAtMi4zLTEtMy42LTEuOGMwLDAtMS43LTEtNC41LTQuN2MwLDAsMC4xLDQuMi00LjQsNi40QzQuNCw5LjMsMCwxNS4yLDAsMjIuN0MwLDMyLjIsNy44LDQwLDE3LjMsNDAKCWM5LjYsMCwxNy4zLTcuOCwxNy4zLTE3LjNDMzQuNywxMS4xLDI0LDYuNiwyNCw2LjZ6IE00LjgsMTYuMWMtMi43LDAuNi0yLjUtMC44LTItMmMwLjItMC43LDAuOS0xLjUsMC45LTEuNWMxLjgtMi45LDUuOC01LDUuOC01CglsMCwwYzAuNS0wLjIsMS40LTAuNywyLjItMS4xYzEuNi0wLjksMi0xLjQsMi0xLjRjMi4zLTIuMiwyLjEtNC45LDIuMS01YzAsMCwwLDAsMCwwYzAsMCwwLDAsMCwwdjBjMCwwLDAsMCwwLDAKCWMyLDQtMC40LDUuOC0wLjQsNS44YzAuNiwwLjYsMC40LDEuMiwwLjQsMS4yQzEyLjcsMTMuOCw0LjgsMTYuMSw0LjgsMTYuMXogTTI1LjcsMzcuMWMtMC4yLDAuMS0yLjcsMS4zLTUuNiwxLjMKCWMtMS42LDAtMy4zLTAuNC00LjgtMS40Yy0wLjUtMC40LTAuNy0xLjEtMC40LTEuNmMwLjEtMC4yLDAuNy0wLjksMi4xLDBsMCwwYzAuMSwwLjEsMy40LDIuMyw4LjUtMC41YzAuNC0wLjIsMC45LTAuMSwxLjEsMC4zCglDMjYuOSwzNS42LDI3LDM2LjQsMjUuNywzNy4xeiBNMTguNywzMi45bDAuMS0wLjFjMC4xLTAuMSwxLjgtMi4zLDQuMy0yYzAuNCwwLDEuOCwwLjEsMi43LDEuOGMwLjEsMC4yLDAuMywwLjktMC4xLDEuNAoJYy0wLjIsMC4yLTAuNSwwLjQtMS4xLDAuMmMtMC40LTAuMS0wLjYtMC41LTAuNi0wLjdsMCwwYy0wLjEtMC4zLTAuMi0wLjUtMS4yLTAuNmMtMC44LTAuMS0xLjMsMC4zLTEuOSwwLjgKCWMtMC4zLDAuMy0wLjcsMC42LTEuMSwwLjdjLTAuMSwwLjEtMC4yLDAuMS0wLjQsMC4xYy0wLjIsMC0wLjQtMC4xLTAuNi0wLjJDMTguNSwzNCwxOC40LDMzLjYsMTguNywzMi45eiBNMzAuMSwzMy4xCgljMCwwLTAuOSwwLjMtMS44LTAuN2MwLDAtMi43LTMuMS00LTMuNmMwLDAtMC44LTAuMy0xLjgsMC4xYzAsMC0wLjcsMC4xLTMuNCwxLjljMCwwLTQuNiwyLjktNi45LDIuNWMwLDAtNS4yLDAuMS00LjUtNS40CgljMCwwLDEuMS02LjIsOC4zLTQuOGMwLDAsMS42LDAuMyw0LjUsMi42YzAsMCwyLDEuNSwzLDEuNWMwLDAsMC44LDAuMSwyLjYtMWMwLDAsMy41LTIuNyw0LjgtMi42YzAsMCwwLDAsMCwwCgljMC4yLDAsMi41LTAuMSwyLjUsMy43QzMzLjMsMjcuMiwzMy40LDMxLjYsMzAuMSwzMy4xeiIvPgo8L3N2Zz4K
  
  # Additional notes displayed in the template's detail view.
  # Each note object is displayed as a small section heading with content below. Supports limited HTML.
  notes:
    - heading: "Apps & Services"
      content: "PHP 7.2<br/>MySQL 10.2"
```

### Template file: initialize

 This key contains the arguments to the environment initialization call. If this isn't included the project will not be initializable from the CLI.

 ```
initialize:
  repository: git://github.com/platformsh/template-drupal7.git@master
  config: null
  files: []
  profile: Drupal 7
```
`repository` is the HTTP Git URL to the repository to be cloned.
`config` currently not available, please use null for its value.
`files` can be a list of file objects that are added to the repository from the template. The spec of a member of `files` is:
```
{
  "mode": 436, # The decimal of the file mode
  "path": "auth.json", # The path of the file in the repository
  "contents": "XXXXXXXX" # The base64-encoded contents of the file
}
```
`profile` is the name used when the environment is initialized (i.e. built for the first time).  

### Template File: defaults

The default key allows the `YAML` file to make additional changes to the project after it has been provisioned but before the subscrition is marked as active. Currently, only two default options are available `variables` and `access`, examples of both can be found below and in the example file above.

``` 
defaults:
  # Here the `variables` key allows default project-level variables to be set. 
  variables:
    - name: env:COMPOSER_AUTH
      value: ""
      is_json: false
      visible_build: true
      visible_runtime: false
    - name: drupal7:site_name
      value: "Hello, world!"
      is_json: false
      visible_build: false
      visible_runtime: true

  # A list of UUIDs and access levels for the project
  access:
    - user: [UUID HERE]
      role: admin
    - user: [UUID HERE]
      role: viewer
    - email: [EMAIL HERE]
      role: admin
    - user: [UUID HERE]
```

### Template File: regions
`regions` allows the list of available regions to be expanded or restricted for a particular project. It accepts three different options: 

`additional` :  This adds regions not in the default list, making them accessible to the user for this project/checkout.
`only`: This key overrides the list provided by the defaults + the additional key, but does not permit access to any excluded regions. For this key, the last implementation of this key will "win".
`exclude`: Removes regions from the list and blocks them from being used for this project.

```
regions:
  additional:
    - bc.platform.sh
  only:
    - us.platform.sh
    - eu.platform.sh
  exclude: 
    - us-2.platform.sh
    - au.platform.sh
    - eu-2.platform.sh
    - nl-1.platform.sh
```

### Template File: plans

`plans` is the same as the behavior of `regions` above, allowing the list of plans to be expanded or reduced. This is useful for ensuring that certain templates can only be provisioned as development projects or that templates with specific resource requirements get a minimum plan size at creation time. It accepts three different options: 

`additional` : This adds regions not in the default list, making them accessible to the user for this project/checkout.

`only`: This key overrides the list provided by the defaults + the additional key. For this key, the last implementation of this key will "win" (i.e. the project level will supersede the vendor level if this key is present.)

`exclude`: Removes plans from the list and bloceks them from being used for this project.

```
plans:
  exclude:
    - development
    - small
    
  additional:
    - 2xlarge
    - xlarge
  only:
    - development
    - standard
    - medium
    - large
```
