SHULKER V2 - SETUP GUIDE (LINUX)
=================================
thanks for purchasing shulker v2. this guide covers everything you need to get
started on linux.


USEFUL LINKS
------------
stats.shulkerv2.xyz  - your live checking dashboard. shows real time stats while the
                       checker is running, including accounts checked, hits found, sniper
                       activity, and DonutSMP autopay totals. you can also see which
                       accounts are currently being targeted by the robux sniper and
                       clear sniped codes from here.

aml.shulkerv2.xyz    - the AML manager. tracks all your auto mark lost accounts and
                       their status. shows when accounts are pending, completed, or
                       canceled. you can check status manually, import existing AML
                       files, get discord notifications on status changes, and manage
                       completed accounts. log in with the same credentials as web stats.


QUICK START
-----------
1. make the binary executable:  chmod +x ShulkerV2
2. open config.json and put your license key in the license_key field
3. put your combos in combos.txt (format: email:password, one per line)
4. put proxies in proxies.txt if you have them (ip:port or ip:port:user:pass)
5. set up webhooks in webhook_config.json if you want discord notifications (optional)
6. run it:  ./ShulkerV2


LINUX REQUIREMENTS
------------------
- any linux distro (ubuntu, debian, centos, arch, etc.)
- no dependencies needed, it's a single binary
- works on VPS, dedicated servers, and local machines
- tested on ubuntu 22.04/24.04 and debian 11/12


FILES
-----
  combos.txt         your account list to check
  proxies.txt        proxy list (optional but strongly recommended)
  config.json        all settings
  webhook_config.json  discord webhook settings
  results/           created automatically, all your hit files go here
  hwid.json          hardware ID file, auto-generated, do not delete


DISPLAY MODES
-------------
when you launch the checker it'll ask you to pick a mode:

  logs mode  - shows every account being checked in real time with full output
  CUI mode   - clean dashboard with live totals and stats, no per-account noise
               recommended for large runs


CONFIG SETTINGS
---------------
all settings are in config.json. here's what each one does:

  license_key               your license key

  threads                   number of concurrent threads. default is 50
  threads_mode              set to Auto to let the checker pick based on your proxies,
                            or Manual to use your threads value directly

  hypixel_check             check hypixel ban status and stats
  donut_check               check donutsmp ban status and stats
  ban_check                 minecraft ban detection
  xbox_perks                grab xbox perk and promo codes
  ms_rewards                check microsoft rewards points
  ms_balance                check microsoft account balance
  auto_mark_lost            automatically mark accounts as lost with a recovery email

  retry_rate_limited        retry accounts that hit microsoft rate limits
  retry_delay_seconds       seconds to wait before retrying a rate limited account
  retry_prompt_timeout_sec  how long to wait on a rate limit prompt before giving up

  set_name                  auto rename accounts eligible for name changes
  name_prefix               prefix for auto renamed accounts (max 8 characters)
  set_skin                  auto set a skin on every account
  skin_img                  url of the skin image to use


RESULT FILES
------------
a results folder is created automatically. files inside:

  all_hits.txt                  everything combined (minecraft + xbox)
  mc_hits.txt                   minecraft java accounts
  mc_capture.txt                minecraft accounts with username and ban status
  mctoken.txt                   minecraft account tokens
  ms_valid.txt                  valid microsoft accounts (no minecraft)
  ms_balance_hits.txt           accounts with a microsoft balance
  xbox_game_pass.txt            accounts with xbox game pass
  xbox_game_pass_ultimate.txt   accounts with xbox game pass ultimate
  all_xbox_codes.txt            all xbox redeem codes found
  valid_xbox_codes.txt          xbox codes that are confirmed valid
  RP_codes.txt                  robux promo codes sniped
  nitro_promo_links.txt         discord nitro promo links
  reward_point_hits.txt         accounts with microsoft reward points
  reward_point_hits_sorted.txt  same but sorted by point balance
  hypixel_stats.txt             hypixel stats for accounts that had them
  hypixel_ban.txt               hypixel banned accounts
  hypixel_unban.txt             hypixel unbanned accounts
  hypixel_ranked.txt            accounts with a hypixel rank
  donut_stats.txt               donutsmp stats
  donut_ban.txt                 donutsmp banned accounts
  donut_unban_online.txt        donutsmp unbanned accounts currently online
  donut_unban_offline.txt       donutsmp unbanned accounts that are offline
  capes.txt                     accounts with minecraft capes
  set_name.txt                  accounts that had their name changed
  auto_mark_lost.txt            accounts marked lost with recovery email info
  invalid.txt                   invalid or dead accounts
  locked.txt                    accounts that are locked
  ban_check_unknown_errors.txt  accounts where ban check hit an error


DISCORD WEBHOOKS
----------------
edit webhook_config.json to set up notifications. you can send different hit types
to different channels, or just use one webhook for everything. leave any field blank
to disable that notification type.

  default_webhook           main channel for MC and Xbox hits
  hypixel_unbanned_webhook  unbanned hypixel accounts only
  hypixel_banned_webhook    banned hypixel accounts only
  donut_unbanned_webhook    unbanned donutsmp accounts only
  donut_banned_webhook      banned donutsmp accounts only
  xbox_hits_webhook         xbox game pass accounts
  nitro_promo               discord nitro promo codes
  xbox_codes                xbox redeem codes

embed options (set true or false):

  bot_name               webhook display name
  include_email          show/hide email
  include_password       show/hide password
  include_hypixel        show/hide hypixel ban status
  include_hypixel_stats  show/hide hypixel stats
  include_donut          show/hide donutsmp ban status
  include_donut_stats    show/hide donutsmp stats
  include_type           show/hide account type (java/xbox)
  include_combo          show/hide email:password combo

embeds are colour coded - green for unbanned, orange for banned, blue for xbox.
email and password are spoilered automatically. tokens are included in hit payloads.


ROBUX SNIPER
------------
the robux sniper automatically watches for microsoft rewards accounts with 7000+
points and redeems them for robux codes. it runs alongside the main checker, nothing
extra to configure.

when a code is sniped you'll hear a sound notification and it shows up on the web
stats dashboard. there's a clear codes button on stats if you want to reset the list.
the dashboard also shows which accounts are currently being targeted.

requires ms_rewards to be enabled in config.json.


DONUTSMP AUTOPAY
----------------
autopay automatically sends donutsmp in-game money from hit accounts to your target
player while checking. set it up in config.json:

  donut_auto_pay.enabled        set to true to enable
  donut_auto_pay.target_player  the donutsmp username to receive the money

the web stats dashboard shows a running total of how much has been sent.
requires donut_check to be enabled.


AML MANAGER (aml.shulkerv2.xyz)
--------------------------------
when the checker successfully marks an account lost it's automatically sent to the
AML manager. you don't need to do anything manually.

log in at aml.shulkerv2.xyz with the same credentials as your web stats account.

tabs:
  pending    accounts waiting for microsoft to process the recovery (~30 days)
  completed  accounts where the security info was successfully replaced
  canceled   accounts where the process was canceled by microsoft

checking status:
  use the Check button on any card to check that account, or Check All to go through
  every pending account at once. Check All shows a live progress bar as it works.
  accounts that have been pending 31+ days are automatically checked every day at noon.

importing:
  if you have an existing auto_mark_lost file from previous runs, click Import in the
  top bar and upload it. the dashboard parses it automatically and only keeps MC
  accounts that have a date.

bin:
  completed accounts can be moved to the bin once you're done. they stay for 5 days
  then get deleted automatically. you can restore them or empty the bin at any time.

discord notifications:
  go to Settings and paste your discord webhook url. you'll get a notification any
  time an account changes status.


PROXIES
-------
- http proxies recommended. socks4 and socks5 are also supported
- 50 threads with good proxies will do 200-300+ accounts per minute
- if you don't have proxies the checker falls back to 1 thread on your own IP
- the checker slows itself down automatically if proxies run low
- VPS in US or EU recommended for best speed


RUNNING IN THE BACKGROUND
--------------------------
to run in the background and keep it going after you disconnect:

using screen (recommended):
  screen -S shulker
  ./ShulkerV2
  press ctrl+a then d to detach
  reconnect later with: screen -r shulker

using tmux:
  tmux new -s shulker
  ./ShulkerV2
  press ctrl+b then d to detach
  reconnect later with: tmux attach -t shulker

using nohup (simpler but no way to reattach):
  nohup ./ShulkerV2 &

to check if it's running:
  ps aux | grep ShulkerV2

to stop it:
  pkill ShulkerV2


TRANSFERRING FILES TO YOUR SERVER
----------------------------------
using WinSCP (windows, easiest):
  download WinSCP, connect to your server, drag and drop the files over.

using scp from powershell or terminal:
  scp ShulkerV2 user@yourserver:/path/to/folder/
  scp combos.txt user@yourserver:/path/to/folder/
  scp proxies.txt user@yourserver:/path/to/folder/
  scp config.json user@yourserver:/path/to/folder/
  scp webhook_config.json user@yourserver:/path/to/folder/


FILE PERMISSIONS
----------------
if you get a permission denied error when trying to run it:
  chmod +x ShulkerV2

if you get errors with config or result files:
  chmod 644 config.json combos.txt proxies.txt webhook_config.json
  chmod 755 .


TROUBLESHOOTING
---------------
"permission denied" when running:
  chmod +x ShulkerV2

"cannot execute binary file":
  make sure you downloaded the linux version, not the windows .exe

"license validation failed" with a network error:
  check your firewall:  ufw allow out 443/tcp
  or temporarily disable it to test:  ufw disable

results folder not being created:
  check write permissions:  chmod 755 .


HWID & LICENSE
--------------
your license binds to your machine on first run. if you need to move to a new server
or PC, contact support with your license key and it'll get reset. do not share or
copy hwid.json between machines. you can reset your own license by /resetmyhwid on discord


AUTO RUN
--------
To skip the startup questions and launch directly with saved settings:
  1. Open config.json and scroll to the "auto_run" section at the bottom
  2. Set "enabled" to true
  3. Fill in the numbers for each setting (1, 2, etc. — options are shown in the key names)
  4. Save and launch — the checker will start immediately with those settings


NAME SETTING
------------
When set_name is enabled, the checker renames accounts automatically.
You can customise the format under the "naming" section in config.json:

  prefix        — text at the start of every name  (e.g. "Sv2")
  suffix        — optional text at the end          (e.g. "YT", or leave empty)
  separator     — character between parts           (e.g. "_", "-", or "" for none)
  use_words     — true/false, adds a random word    (e.g. Wolf, Blade, Frost)
  words         — how many words to include         (1 recommended)
  random_length — length of the random part         (minimum 3, keeps names unique)

A live example of your current format is shown at startup under "Name Format".
If your prefix is too long to fit everything, words are dropped first to make room.
The random part is always kept to guarantee uniqueness.

Example outputs with default settings (prefix=Sv2, sep=_, words=1, random=3):
  Sv2_Wolf_4f2
  Sv2_Frost_x9k
  Sv2_Blade_3mq


PROBLEMS?
---------
if something isn't working, reach out with your license key, the error message, and
which linux distro you're on. most issues get sorted out quickly.

enjoy!
