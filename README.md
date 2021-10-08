# hackgrant
Vagrantfile for hackerstuff.
When I do hackerstuff, especially CTFs, my VMs get cluttered very quickly, and builds up huge amounts of state faster than Russia in the twenties.
To get this mess under control, I now use vagrant and ansible to provision my VM.

The reason I am not using Nix for this is because I want to do reverse engineering, and for reverse engineering you want to be able to run random binaries off the internet, something which Nix does not excel at.
