Android Build System (Cyanogenmod 13/14) + optional && Automated Key-Signing

This repository adds optional && automated key-signing to android_build (cyanogenmod 13/14). By patching the build system, you 
can easily sign your own rom with your own private keys (rather than using test-keys found in the android SDK or using 
Cyanogenmod's release-keys or dev-keys). This may be advantagous for some people who are creating customized CM-based roms,
do not want ot manually re-sign the rom and/or would prefer to not use someone else's keys. 

When you have generated your keys AND pass the environment variable to enable key-signing, the build system will re-sign all of 
your rom, apps and zips and aslo change the build from a test-keys build to a release build. The steps are simple - In bash, from your 'croot' or root directory of AOSP/CM sources;

* $ mkdir keys
* $ cd keys

(You may want to look at the raw file, since github will wrap the below commands!) Format:

    [command] [key type] [C=Country code] [ST=State/Province] [L=City] [O/OU/CN=Rome name] [email address]

../development/tools/make_key releasekey '/C=CA/ST=Ontario/L=Toronto/O=ROM/OU=ROM/CN=ROM/emailAddress=xxxxx@gmail.com'

../development/tools/make_key platform '/C=CA/ST=Ontario/L=Toronto/O=ROM/OU=ROM/CN=ROM/emailAddress=xxxxx@gmail.com'

../development/tools/make_key shared '/C=CA/ST=Ontario/L=Toronto/O=ROM/OU=ROM/CN=ROM/emailAddress=xxxxx@gmail.com'

../development/tools/make_key media '/C=CA/ST=Ontario/L=Toronto/O=ROM/OU=ROM/CN=ROM/emailAddress=xxxxx@gmail.com'

../development/tools/make_key verity '/C=CA/ST=Ontario/L=Toronto/O=ROM/OU=ROM/CN=ROM/emailAddress=xxxxx@gmail.com'

../development/tools/make_key extra '/C=CA/ST=Ontario/L=Toronto/O=ROM/OU=ROM/CN=ROM/emailAddress=xxxxx@gmail.com'

Exporting the environment varilable below points the build system to your keys. (I add it in the script that I use 
for setting up android builds before compililation). NOTE: It must be passed in order for the automated key-singing to be used.
If it is not passed, then android_build will fall back to the regular keys.

$ export SIGNING_KEY_DIR=/path/to/your/signing-keys

    Viola! no more public keys!

REFERENCES:

* https://copperhead.co/android/docs/building
* https://source.android.com/devices/tech/ota/sign_builds.html
