# Julia dev environment using Vagrant

This [Vagrant](https://www.vagrantup.com/) configuration provide dev environment for [Julia](https://julialang.org/).

## Usage

The use of this project is very easy, just execute the following command (Vagrant need to be installed):

```bash
git clone https://github.com/scls19fr/JuliaVagrant
cd JuliaVagrant

# Starts and access VM
vagrant up # it may takes many time
vagrant ssh
```

The directory that map the host is `/srv/`

## Credits

This project was inspired by:
- https://github.com/scls19fr/lua_luarocks_vagrant
