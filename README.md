# SmartLoan Mobile Agent
This dApp is build according to Hyperledger's React Native Mobile Agent.
For details, visit the original repository [here](https://github.com/hyperledger/aries-mobile-agent-react-native).

## Install

### Prerequistes

#### React Native

Installation instructions are documented [here](https://reactnative.dev/docs/environment-setup).

Troubleshooting guides can be found in the [docs/installation](./docs/INSTALLATION.md) directory.

[Cocoa Pods](https://cocoapods.org/) (iOS specific)

```sh
npm install rn-indy-sdk --save
brew install watchman
npm install -g react-native-cli
react-native link rn-indy-sdk
```

#### Mediator

In order to use Aries Bifold, you must have a mediator to use with the app. Instructions for launching your own mediator locally can be found in [docs/mediations](./docs/MEDIATION.md) or at [Aries Framework Javascript](https://github.com/hyperledger/aries-framework-javascript#starting-mediator-agents).

#### Network

Aries Bifold as of right now is tied to one ledger with the intention of making this more flexible/dynamic in the future. You must have a genesis file url for your chosen network, such as:

- Indicio TestNet: https://raw.githubusercontent.com/Indicio-tech/indicio-network/main/genesis_files/pool_transactions_testnet_genesis
- Sovrin StagingNet: https://raw.githubusercontent.com/sovrin-foundation/sovrin/master/sovrin/pool_transactions_sandbox_genesis
- Local network: _TODO: Insert instructions to run local network_

### Running the App via Visual Studio

To run the Android Emulator, install Android Studio and setup emulator version in AVD manager.  
Instructions can be found [here](https://developer.android.com/studio/run/managing-avds).

```sh
git clone https://github.com/SmartLoan/smartloan-mobile-agent
cd smartloan-mobile-agent
```

After clone, install using --force if version error appear:

```sh
npm install --force
```

Export the environmental variables:

```sh
export ANDROID_HOME=$HOME/Library/Android/sdk
export PATH=$PATH:$ANDROID_HOME/emulator
export PATH=$PATH:$ANDROID_HOME/tools
export PATH=$PATH:$ANDROID_HOME/tools/bin
export PATH=$PATH:$ANDROID_HOME/platform-tools
export MEDIATOR_URL=https://dd652a260851.ngrok.io
export GENESIS_URL=https://raw.githubusercontent.com/Indicio-tech/indicio-network/main/genesis_files/pool_transactions_testnet_genesis
```

#### APKs

Sample generated APKs can be found in each github release.

### iOS Specific

Install iOS Pods:

```sh
cd ios
pod install
```

In the /ios directory, open the project workspace file in Xcode.
Once the project is open, navigate to the project's Signing & Capabilities tab and apply your personal Apple Developer Account or your organization's team to target AriesBifold and target AriesBifoldTests.

Adjust the bundle identifier if needed.

Plug in iOS Device

```sh
npm run start
```

#### Run Via Command Line

```sh
npm run ios
```

#### Run Via Xcode

Choose your physical iOS device as the destination.

Click the "Play" button to Build and Run.

#### TestFlight

TODO: Additional community conversation is needed on this topic.

## Troubleshooting

#### Hot Reloading

Hot reloading may not work correctly with instantiated Agent objects. Reloading (`r`) or reopening the app may work. Any changes made to native modules require you to re-run the compile step.

#### Mediator Issues

There are known mediator issues which is undergoing work to address.

### Dependency Issues, Native Module Linking Issues, or Usage Issues

If you end up changing dependencies or structures, you may need to perform the following steps:

#### Android

```sh
rm -rf node_modules
npm install
```

Clean the Android build:

```sh
cd android
./gradlew clean
cd ..
```

Start and clean the Metro cache:

```sh
npm run start
```

In your second terminal, you can now run:

```sh
npm run android
```

## License

[Apache License Version 2.0](./LICENSE)
