# hyprsunder
![logo](hyprsunder.png)
Logo font: [https://velvetyne.fr/fonts/facade/](https://velvetyne.fr/fonts/facade/)

## Background
The Raspberry Pi 4 firmware does not support change the gamma. See this issue: https://github.com/raspberrypi/firmware/issues/1274
<br>
But I really can't live without my blue light filter.
<br><br>
So as a workaround i made this script that utilizes Hyprland's built in shader functionallity. 
<br>
I did not write the shader myself, it's stolen from here: https://github.com/hyprwm/Hyprland/issues/1140#issuecomment-133512843
<br>
hyprsunder is merely a way to change the value of the shaders temperature and temperature strength variables.
<br>
<br>
Some comments with *fake* variables are added to the shaderfile. These are used to store the values during toggling:
```c
// Memory values used by hyprsunder"
// temperatureMem = 2600.0;"
// temperatureStrengthMem = 1.0;"
// stateMem = on;"
```
## Installation
Create this directory if you haven't already:
```sh
mkdir $HOME/.local/bin
```
`git clone` this repo:
```sh
git clone https://github.com/edermats32/hyprsunder.git
```
Copy the files to their default locations:
```sh
cp ./hyprsunder/hyprsunder.glsl $HOME/.config/hypr/
```
```sh
cp ./hyprsunder/hyprsunder $HOME/.local/bin/
```
Make `hyprsunder` executable
```sh
chmod +x $HOME/.local/bin/hyprsunder
```
## Usage
### Parameters
| Parameter       | Short | Description                               |
|-----------------|:-----:|-------------------------------------------|
| `--toggle`      | `-o`  | Change the on/off state (toggle if empty) |
| `--temperature` | `-t`  | Change the temperature                    |
| `--strength`    | `-s`  | Change the temperature strength           |
| `--print`       | `-p`  | Print the current configuration           |
| `--help`        | `-h`  | The help page, basically this             |

*If run without any parameters, it will just load the current configuration.*

### Practical examples
#### Set the temperature and temperature strength
```sh
$HOME/.local/bin/hyprsunder -t <float> -s <float>
```
Example:
```sh
$HOME/.local/bin/hyprsunder -t 2500.0 -s 1.0
```
#### Increase the temperature and temperature strength
```sh
$HOME/.local/bin/hyprsunder -t +<float> -s +<float>
```
Example:
```sh
$HOME/.local/bin/hyprsunder -t +500.0 -s +0.1
```
#### Decrease the temperature and temperature strength
```sh
$HOME/.local/bin/hyprsunder -t -<float> -s -<float>
```
Example:
```sh
$HOME/.local/bin/hyprsunder -t -500.0 -s -0.1
```
#### Toggle on/off
```
$HOME/.local/bin/hyprsunder -o
```
### Hyprland configuration example
```conf
# Start hyprsunder and load the configuration at startup
exec-once = $HOME/.local/bin/hyprsunder

# Some keybind examples
# Only mute works here??? Fuck it, don't care (maybe try sh -c <command> i'm to lazy atm)
#bind = $mainMod, XF86AudioRaiseVolume, exec, $HOME/.local/bin/hyprsunder -t +300.0
#bind = $mainMod, XF86AudioLowerVolume, exec, $HOME/.local/bin/hyprsunder -t -300.0
#bind = $mainMod, XF86AudioForward, exec, $HOME/.local/bin/hyprsunder -s +0.1
#bind = $mainMod, XF86AudioBack, exec, $HOME/.local/bin/hyprsunder -s -0.1
bind = $mainMod, XF86AudioMute, exec, $HOME/.local/bin/hyprsunder -o
```
