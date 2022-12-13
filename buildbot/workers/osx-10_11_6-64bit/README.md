# Install XCode

Installed through App Store.

# Build V8

Same as on Linux but with pointer compression enabled.

# Install Qt

https://download.qt.io/official_releases/online_installers/

Installed Qt 5.12.12 as admin.  Linked to it in ``~buildbot/build`` directory.

# OpenSSL

    curl -fsSLO https://www.openssl.org/source/openssl-3.0.7.tar.gz
    tar xf openssl-3.0.7.tar.gz
    cd openssl-3.0.7
    export MACOSX_DEPLOYMENT_TARGET=10.13
    ./config darwin64-x86_64-cc no-shared
    make -j8

# Install worker

    python3 -m pip install --user --upgrade pip buildbot-worker scons six

Then:
    WORKER="$(python3 -m site --user-base)/bin/buildbot-worker"
    $WORKER create-worker . master.camotics.org:8012 osx-10_11_6-64bit <password>
    $WORKER start

# Unlock keychain

    security unlock-keychain

Then enter login password.

# Allow remote access for all users

    sudo /System/Library/CoreServices/RemoteManagement/ARDAgent.app/Contents/Resources/kickstart \
      -activate -configure -access -on -configure -allowAccessFor -allUsers \
      -configure -restart -agent -privs -all
