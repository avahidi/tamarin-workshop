Cybersecurity lab Tamarin workshop 2019-10-29



Installing Tamarin
------------------

Normally you would want to use your package manager to install Tamarin
(e.g. "apt install tamarin"). But on Ubuntu 18.04 this package is missing and 
you cannot compile it from source due to the unstable Maude dependency.

Hence you will have to install the pre-compiled version (preferably inside a container, see below)::

    sudo apt install -y --no-install-recommends wget unzip graphviz
    mkdir -p ~/.local/bin ~/tmp/tamarin
    cd ~/tmp/tamarin

    
    wget http://maude.cs.illinois.edu/w/images/5/5d/Maude-2.7.1-linux.zip
    wget https://github.com/tamarin-prover/tamarin-prover/releases/download/1.4.1/tamarin-prover-1.4.1-linux64-ubuntu.tar.gz
    unzip Maude-2.7.1-linux.zip
    chmod +x maude.linux64
    mv maude.linux64 maude

    tar xf tamarin-prover-1.4.1-linux64-ubuntu.tar.gz
    mv tamarin-prover maude *.maude ~/.local/bin

And to run it::

    tamarin-prover interactive -p8080 -i'*4'  --debug ~/tmp/tamarin


Using a container
-----------------

You might want to install Tamarin inside a container to keep your main system clean.

Install and configure LXC as described `here <See https://linuxcontainers.org/lxd/getting-started-cli/>`_. 
Then create a clean Ubuntu 18.04 container::

    lxc launch images:ubuntu/18.04 tamarin
    lxc exec tamarin -- useradd -m -s /bin/bash -G sudo -p "" user
    
And enter it::

    lxc exec tamarin -- su -l user -c bash
    