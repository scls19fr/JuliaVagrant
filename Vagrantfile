# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

    julia_major_minor_version = "1.6"
    julia_version = "1.6.3"
    os = "linux"
    isa = "x64"  # instruction set architecture
    isa_full = "x86_64"

    hostname = "julia.box"
    locale = "en_GB.UTF.8"

    # Box
    config.vm.box = "ubuntu/impish64"

    # Shared folder
    config.vm.synced_folder ".", "/srv"

    # Change directory to shared folder directory when connecting using vagrant ssh
    config.ssh.extra_args = ["-t", "cd /srv; bash --login"]

    # Setup
    config.vm.provision "setup", type: "shell", inline: <<-SHELL
        touch .hushlogin
        if ! grep -q "cd /srv" ~/.bashrc ; then 
            echo "cd /srv" >> ~/.bashrc 
        fi
        hostnamectl set-hostname #{hostname} && locale-gen #{locale}
        apt-get update --fix-missing
        apt-get install -q -y build-essential
    SHELL

    # Lang
    ## Julia
    config.vm.provision "julia", type: "shell", privileged: false, inline: <<-SHELL
        echo download
        curl -R -O https://julialang-s3.julialang.org/bin/linux/#{isa}/#{julia_major_minor_version}/julia-#{julia_version}-#{os}-#{isa_full}.tar.gz
        echo untar
        tar -zxf julia-#{julia_version}-#{os}-#{isa_full}.tar.gz
        echo remove .tar.gz file
        rm -f julia-#{julia_version}-#{os}-#{isa_full}.tar.gz
        echo "create symbolic link"
        sudo ln -s /home/vagrant/julia-#{julia_version}/bin/julia /usr/bin/julia
        echo "update registry"
        julia -e 'using Pkg; Pkg.update()'
    SHELL

    # Julia application dependencies
    # config.vm.provision "julia_app_deps", type: "shell", privileged: false, inline: <<-SHELL
    #     sudo apt-get install -q -y system_package_to_install
    #     julia -e 'using Pkg; Pkg.add(["JuliaLibDep1", "JuliaLibDep2"])'
    # SHELL

    # Julia application
    # config.vm.provision "julia_app", type: "shell", privileged: false, inline: <<-SHELL
    #     cd /srv
    #     echo run unit tests
    #     julia -e 'using Pkg; Pkg.test("MyPackage")'
    #     echo run app
    #     julia app.jl
    # SHELL

end