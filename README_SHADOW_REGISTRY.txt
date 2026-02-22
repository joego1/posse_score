Shadow Shooter Registry
=======================

The shadow registry is a persistent list of shooters that carries
across matches. When you add a shooter to a match, the system checks
the shadow registry first and auto-fills their details (name, SASS
number, category, email).

Loading a CSV File
------------------
At the (score) prompt:

  shadow_load example_shadow_registry.csv

CSV Format
----------
First row must be column headers. Recognized columns:

  alias        - Shooter alias (required)
  full_name    - Real name (also: name, fullname)
  sass_number  - SASS membership number (also: sass, sass_no)
  category     - Shooting category (e.g., Cowboy, Senior, Gunfighter)
  email        - Email address (also: e-mail, email_address)

Any additional columns are added to the registry automatically.

Example CSV:

  alias,full_name,sass_number,category,email
  Dusty Trail,William McAllister,10001,Cowboy,dusty.trail@mail.com
  Pecos Belle,Sarah Jane Colton,10002,Lady Senior,pecos.belle@mail.com

Other Shadow Commands
---------------------
  shadow_list           List all shooters in the registry
  shadow_delete <alias> Remove a shooter from the registry
  shadow_save           Add all shooters from current match to registry

Example Files
-------------
  example_shadow_registry.csv      - 6 shooters, 3 categories
  example_shadow_registry_full.csv - 44 shooters, 11 categories
