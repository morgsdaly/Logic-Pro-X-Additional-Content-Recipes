# Logic-Pro-X-Additional-Content-Recipes
Autopkg Recipes for downloading and importing Logic Pro X Additional Content into Munki. Very much just an idea at the moment.

The idea is to first document all the download links for each pkg. From the files installed by the pkg a file needs to be chosen to run `/usr/local/munki/makepkginfo -f /path/to/file` against in order to generate items for an installs list to be added to each pkginfo file. Reference: https://github.com/munki/munki/wiki/How-Munki-Decides-What-Needs-To-Be-Installed 

The resaon for the above is that so far Munki has been trying to reinstall the pkgs unless there is a an installs entry.

The process...
1. Download all the packages viaa fresh Logic Install and obtain them (before installing) via this method: http://www.amsys.co.uk/2015/blog/download-garageband-logic-pro-x-content-loops-deployment/#.VNKTzIbXenM
2. Once the packages are safely copied complete the Logic Installation of the pkgs.
3. Pkg by pkg open the package in Pacifist and expand the file tree to file the first file and it's location.
4. command+i will show you the path to this file... copy that path and run `/usr/local/munki/makepkginfo -f ` against it. This will output the installs list info you need for the Munki pkginfo
5. Document the installs list data with the associated pkg download link.
6. Use the above info to write an Autopkg list.
