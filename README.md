Android Build System (Cyanogenmod 13/14) + optional && Automated Key-Signing

this repository adds optional && automated keysigning to android_build (cyanogenmod 13/14). Currently, cyanogenmod and many 
AOSP-based roms tend to be signed with public keys (like testkey), unless someone has gone to the extra effort to sign their 
builds, which is often a manual process. All of the CM builds are signed with 'testkey' a publicly known key, which is a brutal
security hole and ignores a basic part of Android's security. ie:

if your system apps or OTAs are signed with that test keys, anyone could install a system app or send a malicious OTA and your 
android device would accept it, since it's signed with the correct key! Pretty bad stuff. O_o

By patching the build system, you can easily sign your own rom. The steps are simple - In bash, from your 'croot' or 
root directory of AOSP/CM sources;

* $ mkdir keys
* $ cd keys

Format:    [command] [key type] [Country] [State/Province] [City] [ROM Name/info] [email address]

* $ ../development/tools/make_key releasekey '/C=CA/ST=Ontario/L=Toronto/O=ROM/OU=ROM/CN=ROM/emailAddress=xxxxx@gmail.com'
* $ ../development/tools/make_key platform '/C=CA/ST=Ontario/L=Toronto/O=ROM/OU=ROM/CN=ROM/emailAddress=xxxxx@gmail.com'
* $ ../development/tools/make_key shared '/C=CA/ST=Ontario/L=Toronto/O=ROM/OU=ROM/CN=ROM/emailAddress=xxxxx@gmail.com'
* $ ../development/tools/make_key media '/C=CA/ST=Ontario/L=Toronto/O=ROM/OU=ROM/CN=ROM/emailAddress=xxxxx@gmail.com'
* $ ../development/tools/make_key verity '/C=CA/ST=Ontario/L=Toronto/O=ROM/OU=ROM/CN=ROM/emailAddress=xxxxx@gmail.com'
* $ ../development/tools/make_key extra '/C=CA/ST=Ontario/L=Toronto/O=ROM/OU=ROM/CN=ROM/emailAddress=xxxxx@gmail.com'

Exporting the environment varilable below points the build system to your keys. (I add it in the script that I use 
for setting up android builds). NOTE: It must be passed in order for the automated key-singing to be used. If it is not passed,
then android_build will fall back to the regular keys.

$ export SIGNING_KEY_DIR=/path/to/your/signing-keys

    Viola! no more public keys!

REFS:

* https://copperhead.co/android/docs/building
* https://source.android.com/devices/tech/ota/sign_builds.html
