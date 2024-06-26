## Small Radio Telescope Docs
#### Commands / Command File Syntax

Note: The SRT 2020 software uses a command syntax heavily influenced by the command file syntax of the previous generation's software, which is well documented in [SRT Memo 17](https://www.haystack.mit.edu/wp-content/uploads/2020/07/memo_SRT_017.pdf).  Additionally, the old syntax preceded every command with a ':' character, which is still valid for backwards compatibility.  For the most part, old SRT commands and command files should still be valid.

The SRT software accepts commands in order to change settings at runtime as well as control the running operations.  All commands are funneled into a command queue, which will execute them in order of being received.  Parameters for a command should be separated by spaces.  Most commands are not case sensitive and do not care about excess whitespace.

| Command      | Parameters | Notes |Info                                             |
|--------------|------------|-------|-------------------------------------------------|
| *            | Any text   | 1     | Makes Line a Comment                            |
| stow         | None       |       | Sends the Antenna to Stow                       |
| cal          | None       |       | Sends the Antenna to Calibration Position       |
| calibrate    | None       | 2     | Saves Current Spec as Calibration Data          |
| quit         | None       | 3     | Stows and Gracefully Closes Daemon              |
| record       | [filename] | 4     | Starts Saving into File of Name 'filename'      |
| roff         | None       |       | Ends Current Recording if Applicable            |
| azel         | [az] [el]  |       | Points at Azimuth 'az', Elevation 'el'          |
| offset       | [az] [el]  |       | Offsets from Current Object by 'az', 'el'       |
| freq         | [cf]       |       | Sets Center Frequency in MHz to 'cf'            |
| samp         | [sf]       |       | Sets Sampling Frequency in MHz to 'sf'          |
| wait         | [time]     |       | Stops Execution and Waits for 'time' Secs.      |
| playsound    | [string]   |       | Uses Ubuntu's Speech Dispatcher to declaim text |
| [time]       | None       |       | Waits for 'time' Seconds                        |
| LST:hh:mm:ss | None       |       | Waits Until Next Time hh:mm:ss in UTC           |
| Y:D:H:M:S    | None       |       | Waits Until Year:DayOfYear:Hour:Minute:Sec      |
| [name]       | [n] or [b] | 5     | Points Antenna at Object named 'name'           |

Additional Notes:
 1. Only is considered a comment if the line starts with '\*'.
 2. Calibration takes samples at its current location (which should typically be 'cal') and uses those to determine the shape of the band-pass filter and eliminate it from the calibrated spectra.  Calibration should therefore by done against a non-source object of known noise temperature.
 3. Unlike the previous SRT software, 'quit' both stows and quits (ends the daemon process).  After this is done, it will be necessary to restart the daemon process from command line or via the Dashboard 'Start Daemon' button.
 4. Currently, three different file types are supported, and the type used is determined by the file extension of the name given.  FITS (Calibrated Spectra) is used when the file ends in '.fits', rad (Calibrated Spectra) is used when it ends in '.rad', and Digital RF (Raw I/Q Samples) is used when the name lacks a file ending.  If no filename is provided, Digital RF will be used with an auto-generated name.  In order to use rad or FITS with an autogenerated name, use "\*.rad" or "\*.fits" respectively.
 5. The names used for pointing at objects are set by the 'sky_coords.csv' file, which is further documented in the config folder portion of the docs.  By default, 'Sun' and 'Moon' are already loaded.

##### Building Command Files

Building a command file simply involves putting commands, in order of execution, in a text file.  Only one command can be on a line, as any additional text past the command will be ignored (excluding commands with parameters, which may look past the command statement for additional information).  An example command file is available in the examples/ directory.
