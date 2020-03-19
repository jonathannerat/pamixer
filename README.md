# pamixer: pulseaudio command line mixer

pamixer is like amixer but for pulseaudio. It can control the volume levels of
the sinks.

lso, this project can provide you a small C++ library to control pulseaudio.

## This fork

This fork only introduces upper and lower bounds for volume changes (such as
increase, decrease, set, etc.)

I have my `Vol[+|-]` keys binded to `pamixer --max-volume MAX [-i | -d] 5`, and
`Shift+Vol[+|-]` binded to `pamixer [-i|-d] 5` which causes the following:

- Using `Shift+Vol[+|-]` keys lets me increase/decrease volume unrestrictedly
- With `Vol[+|-]` keys:
  - Volume can't go above MAX
  - If volume is above MAX and is modified, then if new volume is:
  - \> MAX: new volume is set to MAX
  - <= MAX: new volume is preserved

This let\'s us quickly decrease the volume if it's too high. e.g.: volume is
at 100% and MAX=50%, then by pressing `Vol[+|-]` we can set the volume to 50%

## Features

- Get the current volume of the default sink, the default source or a selected one by his id
- Set the volume for the default sink, the default source or any other device
- Set max and min values for volume
- List the sinks
- List the sources
- Increase / Decrease the volume for a device (using gamma correction optionally)
- Mute or unmute a device

## Dependencies

- libpulse
- boost-program_options

## Installation

### From source

  - Get the source
  ```console
    $ git clone https://github.com/cdemoulins/pamixer.git
  ```

  - Compile it
  ```console
    $ make
  ```

  - Or install it
  ```console
    $ sudo make install
  ```
  
  - And use it
  ```console
    $ pamixer --help
    Allowed options:
    -h [ --help ]         help message
    --sink arg            choose a different sink than the default
    --source arg          choose a different source than the default
    --default-source      select the default source
    --get-volume          get the current volume
    --get-volume-human    get the current volume percentage or the string "muted"
    --min-volume arg      prevent following volume changes to go below this value
    --max-volume arg      prevent following volume changes to go above this value
    --set-volume arg      set the volume
    -i [ --increase ] arg increase the volume
    -d [ --decrease ] arg decrease the volume
    -t [ --toggle-mute ]  switch between mute and unmute
    -m [ --mute ]         set mute
    --allow-boost         allow volume to go above 100%
    --gamma arg (=1)      increase/decrease using gamma correction e.g. 2.2
    -u [ --unmute ]       unset mute
    --get-mute            display true if the volume is mute, false otherwise
    --list-sinks          list the sinks
    --list-sources        list the sources
  ```
