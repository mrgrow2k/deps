# Compiler

## Requirements:  

1. Ubuntu 16.0.4.5 AMD 64 Desktop  
2. http://releases.ubuntu.com/16.04/ubuntu-16.04.5-desktop-amd64.iso  
3. 8 Gigs of Ram  
4. 20 Gigs of disk spac

When installing Ubuntu Linux 16.04 AMD64 Desktop you need to create the first user as “spectre”. This should be all lowercase. This is the path in the source files that we will be using to build the software. Do not update to Ubuntu Linux 17 or 18 as this will break software dependencies.  After the system is installed, you need to run the following commands from the desktop of the “spectre” user account.  
 
1. `sudo apt-get update -qq` 
2. `sudo apt-get upgrade -qq`  
3. `sudo apt-get dist-upgrade -qq`  
 
This will ensure that the operating system is up to date and ready to begin. This script is located on our github account for anyone to use freely. Once this has been done, copy and paste the next line into your terminal.  
```wget -O - https://raw.githubusercontent.com/mrgrow2k/compiler/master/doc/ragna.sh | bash```

## Coin Installer

1. Select 1 to update the operating system.  
2. Select 2 to install MXE build Environment  
3. Select 4 to get Spectre Security Source Code  
4. Select 6 to install 3rd party packages  

## Windows QT Wallet 

1. Select 7 to get to the Windows build wallet menu 
2. Select 2 to build the Windows Desktop (QT) Walle


# Manually Building the Windows Wallet 

If you want to manually build the wallet, you can follow the commands below. This needs to be performed in the correct steps. 

1. sudo apt-get update -qq 
2. sudo apt-get upgrade -qq 
3. sudo apt-get dist-upgrade -qq 
4. sudo apt-get install g++-multilib libc6-dev-i386 p7zip-full autoconf automake autopoint bash bison bzip2 cmake flex gettext git g++ gperf intltool libffi-dev libtool libltdl-dev libssl-dev libxmlparser-perl make openssl patch perl pkg-config python ruby scons sed unzip wget xz-utils libtoolbin ruby scons libtool libgdk-pixbuf2.0-dev dos2unix ntp -qq 
5. cd /mnt 
6. sudo git clone https://github.com/mxe/mxe.git 
7. sudo make MXE_TARGETS="i686-w64-mingw32.static" qt 
8. sudo make MXE_TARGETS="i686-w64-mingw32.static" qttools 
9.  sudo make MXE_TARGETS="i686-w64-mingw32.static" boost 
10. cd /mnt/mxe/src 
11. sudo rm openssl.mk 
12. sudo wget https://media.spectresecurity.io/scripts/mxe/openssl.mk 
13. cd .. 
14. sudo make qt5 miniupnpc db boost -j4 MXE_PLUGIN_DIRS=$PWD/plugins/examples/qt5-freeze 
15. sudo make build-only-openssl_i686-w64-mingw32.static 
16. cd /home/spectre/Desktop 
17. git clone https://github.com/mrgrow2k/coinrepo.git 
18. cd /home/spectre/Desktop/ 
19. wget https://github.com/SpectreSecurityCoin/Scripts/raw/master/openssl-1.0.2b.tar.gz  
20. tar -xzvf openssl-1.0.2b.tar.gz 
21. cp -R openssl-1.0.2b openssl-win32-build 
22. cd openssl-win32-build 
23. make clean 
24. chmod -Rv 755 * 
25. export PATH=/mnt/mxe/usr/bin:$PATH 
26. export PATH=$MXEPATH/bin:$PATH 
27. CROSS_COMPILE="i686-w64-mingw32.static-" ./Configure mingw no-asm no-shared -prefix=/mnt/mxe/usr/i686-w64-mingw32.static 
28. make -j4 29. cd /home/spectre/Desktop/ 
30. wget https://github.com/SpectreSecurityCoin/Scripts/raw/master/db-4.8.30.tar.gz 
31. tar -xzvf db-4.8.30.tar.gz 32. cd /home/spectre/Desktop/db-4.8.30 33. make clean 
34. wget https://raw.githubusercontent.com/SpectreSecurityCoin/Scripts/master/berekeydb-4.8.30.sh 
35. dos2unix berekeydb-4.8.30.sh 36. chown -Rv 755 * 
37. export PATH=/mnt/mxe/usr/bin:$PATH 
38. export PATH=$MXEPATH/bin:$PATH 
39. sudo ./berekeydb-4.8.30.sh 
40. cd /home/spectre/Desktop/SpectreSecurityCoin 
41. make clean 
42. cd src/leveldb 
43. make clean 
44. export PATH=/mnt/mxe/usr/bin:$PATH 
45. export PATH=$MXEPATH/bin:$PATH 
46. TARGET_OS=NATIVE_WINDOWS make -j4 CC=i686-w64-mingw32.static-gcc CXX=i686-w64mingw32.static-g++ libleveldb.a libmemenv.a 
47. cd ../.. 48. chmod 775 * -R 
49. cd src/secp256k1 50. make clean 
51. export PATH=/mnt/mxe/usr/bin:$PATH 
52. export PATH=$MXEPATH/bin:$PATH 
53. chmod 775 * -R 
54. ./autogen.sh 55. ./configure --host=i686-w64-mingw32.static --enable-static --disable-shared --enable-modulerecovery 
56. make -j4 
57. cd ../.. 
58. export PATH=/mnt/mxe/usr/bin:$PATH 
59. export PATH=$MXEPATH/bin:$PATH 
60. /mnt/mxe/usr/i686-w64-mingw32.static/qt5/bin/qmake SpectreSecurityCoin.pro 
61. make -j4 

You should now have the coin-qt.exe in the release folder.

## Building Ubuntu Desktop QT Wallet 

You can build the wallet from the following menu by selecting these following options. Once the binary is built, it will be placed in the `~/Desktop/coin/release folder`.

1. Select 8 to get the Windows wallet menu 
2. Select 2 to build the Windows Desktop (QT) Wallet


# Manually Building Ubuntu Desktop QT Wallet 

1. sudo apt-get update -qq 
2. sudo apt-get upgrade -qq 
3. sudo apt-get dist-upgrade -qq 
4. sudo apt-get install g++-multilib libc6-dev-i386 p7zip-full autoconf automake autopoint bash bison bzip2 cmake flex gettext git g++ gperf intltool libffi-dev libtool libltdl-dev libssl-dev libxml-parser-perl make openssl patch perl pkg-config python ruby scons sed unzip wget xzutils libtool-bin ruby scons libtool libgdk-pixbuf2.0-dev dos2unix ntp -qq 
5. cd /mnt 
6. sudo git clone https://github.com/mxe/mxe.git && cd /mnt/mxe/ 
7. sudo make MXE_TARGETS="i686-w64-mingw32.static" qt 
8. sudo make MXE_TARGETS="i686-w64-mingw32.static" qttools 
9. sudo make MXE_TARGETS="i686-w64-mingw32.static" boost 10. cd /mnt/mxe/src 
11. sudo rm openssl.mk 
12. sudo wget https://raw.githubusercontent.com/SpectreSecurityCoin/Scripts/master/openssl.mk 
13. cd .. 
14. sudo make qt5 miniupnpc db boost -j4 MXE_PLUGIN_DIRS=$PWD/plugins/examples/qt5-freeze 
15. sudo make build-only-openssl_i686-w64-mingw32.static 
16. cd /home/spectre/Desktop 
17. git clone https://github.com/mrgrow2k/coinrepo.git 
18. cd /home/spectre/Desktop/ 
19. wget https://github.com/mrgrow2k/deps/releases/download/1.0.2d/openssl-1.0.2b.tar.gz 
20. tar -xzvf openssl-1.0.2b.tar.gz 
21. cp -R openssl-1.0.2b openssl-win32-build 
22. make clean 
23. cd openssl-win32-build 
24. export PATH=/mnt/mxe/usr/bin:$PATH 
25. export PATH=$MXEPATH/bin:$PATH 
26. CROSS_COMPILE="i686-w64-mingw32.static-" ./Configure mingw no-asm no-shared -prefix=/mnt/mxe/usr/i686-w64-mingw32.static 
27. sudo make depend 
28. make -j4 
29. cd /home/spectre/Desktop/ 
30. wget https://github.com/mrgrow2k/deps/releases/download/4.8.30/db-4.8.30.NC.tar.gz 
31. tar zxvf db-4.8.30.NC.tar.gz
32. cd /home/spectre/Desktop/db-4.8.30.NC
33. make clean 
34. wget https://raw.githubusercontent.com/mrgrow2k/deps/master/berekeydb-4.8.30.sh
35. export PATH=/mnt/mxe/usr/bin:$PATH 
36. export PATH=$MXEPATH/bin:$PATH 
37. dos2unix berekeydb-4.8.30.sh 
38. chmod ugo+x berekeydb-4.8.30.sh 
39. sudo ./berekeydb-4.8.30.sh 
40. cd /home/ragna/Desktop/coinrepo
41. make clean 
42. cd src/leveldb 
43. dos2unix  
44. export PATH=/mnt/mxe/usr/bin:$PATH 
45. export PATH=$MXEPATH/bin:$PATH 
46. TARGET_OS=NATIVE_WINDOWS make -j4 CC=i686-w64-mingw32.static-gcc CXX=i686-w64mingw32.static-g++ libleveldb.a libmemenv.a 
47. cd ../.. 
48. chmod 775 * -R 
49. cd src/secp256k1 
50. make clean 
51. export PATH=/mnt/mxe/usr/bin:$PATH 
52. export PATH=$MXEPATH/bin:$PATH 
53. chmod 775 * -R 
54. ./autogen.sh 
55. ./configure --host=i686-w64-mingw32.static --enable-static --disable-shared --enable-modulerecovery 
56. make -j4 
57. cd ../.. 
58. sudo apt-get install build-essential libtool autotools-dev automake pkg-config libssl-dev libeventdev bsdmainutils libgmp-dev libboost-system-dev libboost-filesystem-dev libboost-chronodev libboost-program-options-dev libboost-test-dev libboost-thread-dev libboost-all-dev -qq 
59. sudo apt-get install software-properties-common 
60. sudo add-apt-repository ppa:bitcoin/bitcoin 
61. sudo apt-get update -qq 
62. sudo apt-get install libdb4.8-dev libdb4.8++-dev libminiupnpc-dev libzmq3-dev -qq 
63. sudo apt-get install libqt5gui5 libqt5core5a libqt5dbus5 qttools5-dev qttools5-dev-tools -qq 
64. make clean 
65.  
66. export PATH=/mnt/mxe/usr/bin:$PATH 
67. export PATH=$MXEPATH/bin:$PATH 
68. qmake linux.pro 69. make -j4 


## Building the Linux Daemon 

To build the Linux daemon for application use, please follow the steps below. You will need a VPS with the following requirements. 
1. Ubuntu 16.04.5 Server ( ubuntu-16.04.5-server-amd64.iso ) 
2. 1 Gig ram 
3. 1 core processor 

When you have installed the main Ubuntu server OS, please use these instructions to build the daemon software.

1. apt-get install build-essential libtool autotools-dev automake pkg-config libssl-dev libevent-dev bsdmainutils libgmp-dev -qq 
2. apt-get install libboost-system-dev libboost-filesystem-dev libboost-chrono-dev libboostprogram-options-dev libboost-test-dev libboost-thread-dev libboost-all-dev -qq 
3. apt-get install software-properties-common 
4. add-apt-repository ppa:bitcoin/bitcoin 
5. apt-get update -qq 
6. apt-get install libdb4.8-dev libdb4.8++-dev  libminiupnpc-dev libzmq3-dev -qq 
7. git clone https://github.com/mrgrow2k/coinrepo.git 
8. cd coinrepo/src 
9. make -j4 -f makefile.unix


## MAC OS X:  High Serra 10.13.3 DMG QT Build 

# Requirements: 

1. MAC OS X High Serra 
a. Version 10.13.3 2. Install XCODE 8.1 (or higher 9.2 tested) a. `https://itunes.apple.com/us/app/xcode/id497799835?mt=12` 
3. Install Qt Creator 5.10.1 
4. Install GIT a. `http://mac.github.com/` 
5. Install Brew a. `/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`

1. sudo xcode-select –install 
2. brew install automake berkeley-db4 libtool boost miniupnpc openssl pkg-config protobuf python qt libevent qrencode librsvg cmake autoconf libtool gcc automake  
3. git clone https://github.com/mrgrow2k/coinrepo.git 
4. cd coinrepo 
Your environment should now be set up and ready to compile the SpectreSecurityCoin QT Mac Wallet. 
5. make clean 
6. export CPPFLAGS="-I/usr/local/opt/openssl/include" 
7. export LDFLAGS="-L/usr/local/opt/openssl/lib" 
8. qmake -spec macx-g++ macos.pro 
9. make -j4