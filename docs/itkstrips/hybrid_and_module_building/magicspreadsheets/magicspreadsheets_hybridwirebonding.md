# Hybrid Wire Bonding
The bash script for hybrid wire bonding is called _run_wirebonding_hybrids_bhm.sh_. When you come to run the code, you should edit this script to ensure you’ve set the command line arguments correctly before running it. To do this, you can open the code in a text editor called _emacs_ using the command:
```
emacs run_wirebonding_hybrids_bhm.sh &
```
If you are working remotely (e.g. at home or in the office) you won’t be able to open _emacs_ in a separate window, so you will instead need to run:
```
emacs -nw run_wirebonding_hybrids_bhm.sh
```
Which will open _emacs_ in a command-line window rather than a separate window.
Once you’ve opened the script you will see that it has 5 lines (three with any actual content.) The bit that actually runs the assembly code is line 5. When you come to run the code, you should edit this line depending on what you want to run. The options are listed in the table below:

| Argument (short / long) | Example | Description | Required? |
| ----------------------- | ------- | ----------- | --------- |
| -h --help | -h | Adding this option stops the code from running, and instead displays a help message showing all the command line arguments and their descriptions. | No |
| -d --debug | -d | Adding this option will activate the debug messages. Without it, most debug messages will not be shown. | No, unless there’s a bug you can’t find. |
| -s --sheet_name | -s “My Google Sheet” | This option sets the name of the Google Sheet you are reading from (The one in the top-right). | Yes |
| -t --tab_name | -t "Panel999_Use1_X_P0” | This option sets the name of the Google Sheet tab you are reading from, which corresponds to the hybrid you are using. | Yes |
| -c --itk_credentials_file | -c “credentials/credentials.yml” | This option lets you set the path to the file for your database credentials. The example given on the right has Robbie’s credentials, so the database uploads would be in his name. | Yes, unless you have set options -i and -j instead. |
| -i --itkdb_accesscode_1 | -i "MyPassword1" | This option lets you set the first of your two database access codes, as an alternative to a credentials file. | Only if you haven’t used the -c option. |
| -j --itkdb_accesscode_2 | -j "MyPassword2" | This option lets you set the second of your two database access codes, as an alternative to a credentials file. | Only if you haven’t used the -c option. |

Once you have edited the bash script to the right argument variables using the table above, you will need to save. To do this in _emacs_, you press _Ctrl-x_ followed by _Ctrl-s_. If you want to close _emacs_, the command is _Ctrl-x_ followed by _Ctrl-c_, but this is optional unless it’s in a command line window.
Then, you just run the script using:
```
source run_wirebonding_hybrids_bhm.sh
```
and watch it go! (Taking note of the info and any warning/error messages you get…)
There are a lot of checks at the beginning of this script to make sure that the hybrid has everything uploaded up to this point before the wire bonding is also uploaded.
