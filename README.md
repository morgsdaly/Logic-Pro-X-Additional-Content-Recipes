# Logic-Pro-X-Additional-Content-Recipes

**UPDATE:** Thanks to some good advice from Greg Neagle this is probably the wrong way to go about it. If the packages were being regulary updated then this might be a good idea but they are not. A better idea would be to extend Hannes' work: https://github.com/hjuutilainen/adminscripts/blob/master/download-logicprox-content.py and add the functionality to push the packages to munki after downloading them. Originally too I thought that installs keys would be required. As this info is in the pkgs from apple it might be little trouble to add them anyway, but I have also been advised that if pkg receipts have not been working it's probably due to this bug: https://groups.google.com/forum/#!topic/munki-dev/0Ku-dUjQooQ (There is discussion about updating munki in relation to dealing with this, but in the meantime it may have to be done manually if it cannot be scripted.)

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

Reference files for this project are:

**logicpro1000_en.plist**  
This is the plist file that Logic supposedly uses to know what to download. It can be found at this url http://audiocontentdownload.apple.com/lp10_ms3_content_2013/logicpro1000_en.plist but I suspect that it might be outdated now or not the only file that Logic Pro X is looking too as this plist references 57 packages and Logic actually downloads 60 in total now. My guess is that we still need to find the other plist or the updated version of this one. My other guess is that these will provide a way for us to check our download urls and to track changes between Logic Pro X versions.

**lp10_ms3_content_2013.txt** & **lp10_ms3_content_2015.txt**  
These files simply contain the raw download urls.

**lp10_ms3_content_2013_w_instals.txt** & **lp10_ms3_content_2015_w_instals.txt**  
These files contact the package download urls and the associated installs key data for each pkg.

**Update February 10, 2015**  
My download and munki recipes seem to work. Turns out that all I needed was the download URL and a path for a file for the installs item. Now how best to structure things before writing all the scripts.
