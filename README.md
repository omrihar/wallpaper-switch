# Wallpaper switch

Every day a new picture from: [Astronomy Picture of the Day](http://apod.nasa.gov/apod/astropix.html)

## Content of the repository

- `wallpaper-switch.go` - the acctual application
- `wallpaper-switch.service` - systemd service
- `wallpaper-switch.timer` - systemd timer

## How it works

`wallpaper-switch` checks the RSS feed from NASA's [Astronomy Picture of the Day](http://apod.nasa.gov/apod/astropix.html) and, for a new content, sets a desktop background using `gsettings` command.

It stores its status (file `status.toml`) and the current desktop wallpaper in `"XDG_DATA_HOME/wallpaper-switch"` or, if the envrionment variable is not set, in `".local/share/wallpaper-switch"`.

## How to install

- Install Go (if you don't have it):

`sudo pacman -S go`

Create a directory to store go source code fetched from other repositories

`mkdir -p ~/repos/gosource`

and add it to the `$GOPATH` environment variable.

- Install dependencies:

`go get -u github.com/naoina/toml`

`go get -u github.com/nu7hatch/gouuid`

`go get -u golang.org/x/net/html`

- compile:

`go build wallpaper-switch.go`

- place files `wallpaper-switch.timer` and `wallpaper-switch.service` in `~/.local/share/systemd/user`

- modify variable `ExecStart` in `wallpaper-switch.service` - it should point to a binary of wallpaper-switch.

Then, execute the following commands:

`systemctl --user enable wallpaper-switch.timer`
`systemctl --user start wallpaper-switch.timer`
