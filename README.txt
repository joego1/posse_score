==============================================================================
  POSSE SCORE v1.0 - User Guide
==============================================================================

  Posse-based match scoring for Cowboy Action Shooting.

  Copyright (c) 2026 Joseph Michael Goforth
  Licensed under the MIT License (see LICENSE)

==============================================================================
  CONTENTS
==============================================================================

  1. Getting Started
  2. How It Works - CLI vs Web Server
  3. Typical Match Day Workflow
  4. CLI Command Reference
  5. Web Server
  6. Scoring
  7. Printing Results
  8. Importing & Exporting Data
  9. Distributed Scoring (Multiple Devices)
  10. Tips

==============================================================================
  1. GETTING STARTED
==============================================================================

  WINDOWS:
    Double-click posse_score.exe

  LINUX:
    Open a terminal and run:
      ./posse_score

  The program starts in CLI (command line) mode with the prompt:

    (score)

  Type 'help' to see all available commands.

==============================================================================
  2. HOW IT WORKS - CLI vs WEB SERVER
==============================================================================

  Posse Score has two interfaces that work together:

  CLI (Command Line Interface)
  ----------------------------
  The CLI is the primary administration tool. Use it to:
    - Create and manage matches
    - Add and organize shooters
    - Import/export data
    - Configure printing
    - Start/stop the web server
    - View detailed results

  Web Server
  ----------
  The web server provides a simple browser-based interface designed
  for scoring at the firing line. Posse leaders or scoring helpers
  can connect from phones, tablets, or any device with a browser.

  The web interface is intentionally simple - it focuses on:
    - Selecting a shooter
    - Entering a score (time, misses, penalties, bonuses)
    - Viewing stage and match results

  Match administration (creating matches, managing shooters, importing
  data, configuring printers) is done through the CLI.

  To start the web server from the CLI:

    (score) start_web

  The server displays a URL that other devices can connect to:

    ==================================================
      WEB SCORING SERVER STARTED
    ==================================================
      URL: http://192.168.1.100:5000

      Scorers can connect from phones/tablets
      using a web browser.
    ==================================================

  All devices must be on the same WiFi network.

==============================================================================
  3. TYPICAL MATCH DAY WORKFLOW
==============================================================================

  BEFORE THE MATCH:

    1. Start the program
    2. Create a match:
         (score) create_match Saturday Monthly
    3. Add stages:
         (score) add_stage 1 Livery Stable
         (score) add_stage 2 Saloon
         ...
    4. Add shooters:
         (score) add_shooter DUKE
         (score) add_shooter LEFTY
         ...
       Or import from CSV:
         (score) import shooters.csv

  AT THE RANGE:

    5. Start the web server:
         (score) start_web
    6. Give posse leaders the URL to connect from their devices
    7. Select the posse and stage:
         (score) posse 1
         (score) stage 1
    8. Score shooters (CLI or web):
         (score) 25.32 1 0
         (this enters: 25.32 seconds, 1 miss, 0 penalties)
    9. Advance stages:
         (score) next_stage

  AFTER THE MATCH:

    10. View results:
          (score) results
    11. Print results:
          (score) cups_print
    12. Export to CSV:
          (score) export

==============================================================================
  4. CLI COMMAND REFERENCE
==============================================================================

  MATCH MANAGEMENT
  --------------------------------------------------------------------------
  create_match, cm <name>        Create a new match
  select_match, sm <id|name>     Select the active match
  clone_match, clm <src> <new>   Clone a match structure (without scores)
  delete_match <id|name>         Delete a match
  list, ls                       List all matches
  init                           Initialize database

  SHOOTER MANAGEMENT
  --------------------------------------------------------------------------
  add_shooter, as <alias>        Add shooter to the current posse
                                 (Tab key autocompletes from saved shooters)
  shooter, s <alias|#>           Select a shooter by alias or roster number
  next, n [score]                Select the next unscored shooter
  roster, r                      Show the posse roster
  edit_shooter, es <alias>       Edit shooter details
  delete_shooter, ds <alias>     Delete shooter from database entirely
  remove_shooter, rs <alias>     Remove shooter from current match
  move_shooter, ms <alias> <p>   Move shooter to a different posse
  change_posse, cp <alias> <p>   Change shooter's posse assignment
  shooter_swap <n1> <n2>         Swap two shooters' roster positions
  shooter_insert <alias> <n>     Insert a shooter at a specific position
  set_order, so <n1> <n2>...     Set custom shooting order
  reorder, ro [stage]            Reorder shooters by entry order

  STAGE & POSSE NAVIGATION
  --------------------------------------------------------------------------
  stage, st <number>             Switch to a stage
  next_stage, ns                 Advance to the next stage
  add_stage, ast <#> [name]      Add a stage to the match
  posse, p <number>              Switch to a posse

  SCORING
  --------------------------------------------------------------------------
  score, sc <raw> [m] [p] [b]    Enter a score for the selected shooter
                                   raw = time in seconds
                                   m   = number of misses (5s each)
                                   p   = number of procedural penalties (10s each)
                                   b   = number of bonuses (-5s each)

  You can also type a score directly without the 'score' command:
    (score) 25.32 1 0            Same as: score 25.32 1 0

  SDQ                            Stage Disqualification (150 second penalty)
  MDQ                            Match Disqualification (999 second penalty)
  DNF                            Did Not Finish (999 seconds)

  auto_decimal, ad [on|off]      Toggle auto-decimal placement
                                 When on, typing 2532 becomes 25.32
  auto_advance, aa [on|off]      Toggle auto-advance to next shooter

  RESULTS
  --------------------------------------------------------------------------
  results, res [audit|category]  Show match results
  summary, sum                   Show match summary

  SHADOW REGISTRY
  --------------------------------------------------------------------------
  The shadow registry saves known shooters so you can quickly add
  them to future matches using Tab autocompletion.

  shadow_list                    List all saved shooters
  shadow_add                     Add current match shooters to registry
  shadow_clear                   Clear the registry

  PRINTING
  --------------------------------------------------------------------------
  Thermal (receipt) printers:
    thermal_print [mode]         Print to USB thermal printer (ESC/POS)
    set_thermal_printer          Configure USB thermal printer device
    bt_setup                     Configure Bluetooth thermal printer
    bt_print [mode]              Print to Bluetooth thermal printer
    set_bt_printer <dev> [baud]  Set Bluetooth device path and baud rate

  Standard (full-page) printers:
    cups_print [mode]            Print to any CUPS printer (USB/WiFi/network)
    set_cups_printer             Configure CUPS printer
    set_wifi_printer <name>      Configure WiFi/network printer
    test_wifi_printer            Send test page to WiFi printer

  Other:
    print_and_open [mode]        Print to file and open share menu
    export_email_list            Export semicolon-separated email list
                                 Saves to <MatchName>_email_list.txt
                                 Paste into your email program's recipients field

  Print modes: summary, full, category

  WEB SERVER
  --------------------------------------------------------------------------
  start_web [port]               Start the web scoring interface
                                 (default port: 5000)
  stop_web                       Stop the web server
  web_status                     Show web server status and URL
  web_verbose [on|off]           Toggle HTTP request logging

  IMPORT & EXPORT
  --------------------------------------------------------------------------
  import, imp <file> [name]      Import match data from a CSV file
  export, ex [file]              Export results to CSV
  export_posse, ep [#]           Export a single posse's scores
  merge_posse <file>             Merge CSV scores from another device

  OTHER
  --------------------------------------------------------------------------
  help [cmd]                     Show help (or detailed help for a command)
  quit                           Exit the program

  SHORTCUT: Press Enter with no command to see unscored shooters.
  SHORTCUT: Press Tab to autocomplete shooter aliases.

==============================================================================
  5. WEB SERVER
==============================================================================

  The web server is a companion to the CLI. It provides a mobile-friendly
  interface for entering scores during a match.

  Starting:
    (score) start_web

  Stopping:
    (score) stop_web

  Check status:
    (score) web_status

  The web interface allows scorers to:
    - Select a match, stage, and posse
    - Pick a shooter from the roster
    - Enter time, misses, penalties, and bonuses
    - View stage results and overall standings
    - Move to the next stage when complete

  All data entered through the web interface is saved to the same
  database used by the CLI. Both interfaces stay in sync.

==============================================================================
  6. SCORING
==============================================================================

  Each score consists of:
    - Raw time (seconds, e.g. 25.32)
    - Misses (each miss adds 5 seconds)
    - Procedural penalties (each adds 10 seconds)
    - Bonuses (each subtracts 5 seconds)

  Examples from the CLI:

    (score) 25.32              Time only, no misses or penalties
    (score) 25.32 1 0          25.32 seconds, 1 miss, 0 penalties
    (score) 30.00 2 1          30.00 seconds, 2 misses, 1 penalty
    (score) 22.50 0 0 1        22.50 seconds, 0 misses, 0 penalties, 1 bonus

  Special scores:
    (score) SDQ                Stage disqualification (150s)
    (score) MDQ                Match disqualification (999s for all stages)
    (score) DNF                Did not finish (999s)

  Auto-decimal mode (toggle with 'ad'):
    When enabled, entering 2532 is automatically converted to 25.32.
    This speeds up data entry on devices without a decimal key.

  Auto-advance mode (toggle with 'aa'):
    When enabled, the program automatically moves to the next
    unscored shooter after entering a score.

==============================================================================
  7. PRINTING RESULTS
==============================================================================

  Posse Score supports several printing options:

  CUPS (USB, WiFi, or network printers):
    (score) set_cups_printer    Configure your printer
    (score) cups_print          Print full results

  Thermal receipt printers (USB):
    (score) set_thermal_printer Configure the printer
    (score) thermal_print       Print results

  Thermal receipt printers (Bluetooth):
    (score) bt_setup            Pair and configure
    (score) bt_print            Print results

  Print modes control what is printed:
    cups_print summary          Rankings only
    cups_print full             All stage details
    cups_print category         Results grouped by category

==============================================================================
  8. IMPORTING & EXPORTING DATA
==============================================================================

  IMPORTING:
    To import shooter and match data from a CSV file:
      (score) import myfile.csv
      (score) import myfile.csv "Match Name"

  EXPORTING:
    To export match results to a CSV file:
      (score) export
      (score) export results.csv

    To export a single posse:
      (score) export_posse 1

  COMMAND LINE USAGE:
    You can also run commands directly without entering interactive mode:
      ./posse_score --import-csv myfile.csv
      ./posse_score --list
      ./posse_score --results "Saturday Monthly"
      ./posse_score --export "Saturday Monthly"

==============================================================================
  9. DISTRIBUTED SCORING (MULTIPLE DEVICES)
==============================================================================

  For larger matches, scoring can be split across multiple devices:

    1. Set up the match on the master device (add stages, shooters)
    2. Export each posse:
         (score) export_posse 1
         (score) export_posse 2
    3. Give each posse leader their CSV file
    4. Each device scores independently
    5. After scoring, collect the CSV files from each device
    6. Merge them on the master:
         (score) merge_posse posse1_scores.csv
         (score) merge_posse posse2_scores.csv

  Alternatively, if all devices are on the same WiFi network,
  multiple scorers can connect to the web server simultaneously
  and score in real time.

==============================================================================
  10. TIPS
==============================================================================

  - Press Enter at the (score) prompt to see which shooters still
    need scores for the current stage.

  - Press Tab to autocomplete shooter aliases. This uses the shadow
    registry - run 'shadow_add' after a match to save all aliases
    for next time.

  - Use 'auto_decimal on' if scoring on a device without an easy
    decimal point key. Type 2532 instead of 25.32.

  - Use 'auto_advance on' to automatically move to the next shooter
    after entering a score. This speeds up data entry significantly.

  - The web server and CLI share the same database. You can use both
    at the same time - enter scores on phones via the web and manage
    the match from the CLI.

  - Back up your data regularly. The database file is stored in the
    same directory as the program.

==============================================================================
