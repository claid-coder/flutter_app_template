# Install Node.js

firebase-tools를 설치해야됨

## NVM 설치
% curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash
% Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
Dload  Upload   Total   Spent    Left  Speed
100 16563  100 16563    0     0   401k      0 --:--:-- --:--:-- --:--:--  462k
=> nvm is already installed in /Users/jaeminko/.nvm, trying to update using git
=> => Compressing and cleaning up git repository

=> nvm source string already in /Users/jaeminko/.zshrc
=> bash_completion source string already in /Users/jaeminko/.zshrc
=> You currently have modules installed globally with `npm`. These will no
=> longer be linked to the active version of Node when you install a new node
=> with `nvm`; and they may (depending on how you construct your `$PATH`)
=> override the binaries of modules installed with `nvm`:

/usr/local/lib
├── corepack@0.23.0
├── firebase-tools@13.2.1
=> If you wish to uninstall them at a later point (or re-install them under your
=> `nvm` node installs), you can remove them from the system Node as follows:

     $ nvm use system
     $ npm uninstall -g a_module

=> Close and reopen your terminal to start using nvm or run the following to use it now:

export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion
% source ~/.nvm/nvm.sh
% nvm --version
0.40.1

## Node.js update
% nvm install 22                                                                 
Downloading and installing node v22.13.1...
Downloading https://nodejs.org/dist/v22.13.1/node-v22.13.1-darwin-arm64.tar.xz...
############################################################################################################################### 100.0%
Computing checksum with sha256sum
Checksums matched!
Now using node v22.13.1 (npm v10.9.2)
% node -v
v22.13.1
% npm -v
10.9.2

## NPM upgrade
% npm install -g npm
removed 11 packages, and changed 43 packages in 2s
24 packages are looking for funding
run `npm fund` for details
% npm -v            
11.1.0

## firebase-tools

```shell
% npm install -g firebase-tools

added 635 packages in 25s

70 packages are looking for funding
  run `npm fund` for details
% firebase --version
13.2.1
```

## firebase functions setting

```
% firebase init
(node:57777) [DEP0040] DeprecationWarning: The `punycode` module is deprecated. Please use a userland alternative instead.
(Use `node --trace-deprecation ...` to show where the warning was created)

     ######## #### ########  ######## ########     ###     ######  ########
     ##        ##  ##     ## ##       ##     ##  ##   ##  ##       ##
     ######    ##  ########  ######   ########  #########  ######  ######
     ##        ##  ##    ##  ##       ##     ## ##     ##       ## ##
     ##       #### ##     ## ######## ########  ##     ##  ######  ########

You're about to initialize a Firebase project in this directory:

  /Users/jaeminko/Workspace/CursorStudy/copy_voice_chat

? Which Firebase features do you want to set up for this directory? Press Space to select features, then Enter to confirm your 
choices. (Press <space> to select, <a> to toggle all, <i> to invert selection, and <enter> to proceed)
❯◯ Realtime Database: Configure a security rules file for Realtime Database and (optionally) provision default instance
 ◯ Firestore: Configure security rules and indexes files for Firestore
 ◯ Functions: Configure a Cloud Functions directory and its files
 ◯ Hosting: Configure files for Firebase Hosting and (optionally) set up GitHub Action deploys
 ◯ Hosting: Set up GitHub Action deploys
 ◯ Storage: Configure a security rules file for Cloud Storage
 ◯ Emulators: Set up local emulators for Firebase products
(Move up and down to reveal more choices)

방향키로 Functions로 가서, spacebar로 라디오 버튼 활성화
❯◉ Functions: Configure a Cloud Functions directory and its files

? Which Firebase features do you want to set up for this directory? Press Space to select features, then Enter to confirm your 
choices. Functions: Configure a Cloud Functions directory and its files

=== Project Setup

First, let's associate this project directory with a Firebase project.
You can create multiple project aliases by running firebase use --add, 
but for now we'll just set up a default project.

? Please select an option: (Use arrow keys)
❯ Use an existing project 
  Create a new project 
  Add Firebase to an existing Google Cloud Platform project 
  Don't set up a default project

방향키로 Use an existing project 선택 후 엔터
(firebase에 프로젝트 생성되어 있어야 함)

? Please select an option: Use an existing project
(node:58041) [DEP0044] DeprecationWarning: The `util.isArray` API is deprecated. Please use `Array.isArray()` instead.
? Select a default Firebase project for this directory:  
❯ copy-voice-chat (copy-voice-chat) 

현재 프로젝트인 copy-voice-chat 선택

? Select a default Firebase project for this directory: copy-voice-chat (copy-voice-chat)
i  Using project copy-voice-chat (copy-voice-chat)

=== Functions Setup
(시간 약간 걸림)
Let's create a new codebase for your functions.
A directory corresponding to the codebase will be created in your project
with sample code pre-configured.

See https://firebase.google.com/docs/functions/organize-functions for
more information on organizing your functions using codebases.

Functions can be deployed with firebase deploy.

? What language would you like to use to write Cloud Functions? (Use arrow keys)
❯ JavaScript 
  TypeScript 
  Python

방향키로 JavaScript. 엔터

? What language would you like to use to write Cloud Functions? JavaScript
? Do you want to use ESLint to catch probable bugs and enforce style? (y/N) 그냥 엔터
? Do you want to install dependencies with npm now? Yes

위와 같이 설정

npm warn EBADENGINE Unsupported engine {
npm warn EBADENGINE   package: undefined,
npm warn EBADENGINE   required: { node: '18' },
npm warn EBADENGINE   current: { node: 'v22.13.1', npm: '11.1.0' }
npm warn EBADENGINE }
npm warn deprecated inflight@1.0.6: This module is not supported, and leaks memory. Do not use it. Check out lru-cache if you want a good and tested way to coalesce async requests by a key value, which is much more comprehensive and powerful.
npm warn deprecated glob@7.2.3: Glob versions prior to v9 are no longer supported
npm warn deprecated glob@8.1.0: Glob versions prior to v9 are no longer supported
npm warn deprecated google-p12-pem@4.0.1: Package is no longer maintained

added 529 packages, and audited 530 packages in 25s

57 packages are looking for funding
  run `npm fund` for details

4 critical severity vulnerabilities

To address all issues (including breaking changes), run:
  npm audit fix --force

Run `npm audit` for details.

i  Writing configuration info to firebase.json...
i  Writing project information to .firebaserc...

✔  Firebase initialization complete!
```

## flutterfire configure

```
% flutterfire configure
? You have an existing `firebase.json` file and possibly already configured your project for
Firebase. Would you prefer to reuse the values in your existing `firebase.json` file
to configure your project? (y/n) › no ← no 입력해야함

 ⠹ Fetching available Firebase projects...                                                                                            
i Found 4 Firebase projects. Selecting project copy-voice-chat.                                                                       
? Which platforms should your configuration support (use arrow keys & space to select)? ›                                             
✔android
✔ios
  macos
  web                                  
  windows

android, ios 선택되어 있으면 엔터

✔ Which platforms should your configuration support (use arrow keys & space to select)? · android, ios                                
i Firebase android app com.innorabbit.copy_voice_chat is not registered on Firebase project copy-voice-chat.                          
i Registered a new Firebase android app on Firebase project copy-voice-chat.                                                          
i Firebase ios app com.innorabbit.copyVoiceChat is not registered on Firebase project copy-voice-chat.                                
i Registered a new Firebase ios app on Firebase project copy-voice-chat.                                                              

Firebase configuration file lib/firebase_options.dart generated successfully with the following Firebase apps:

Platform  Firebase App Id
android   1:*****46*****:android:*****a7a1b5ab4789*****
ios       1:*****46*****:ios:*****87bfd2b770e9*****

Learn more about using this file and next steps from the documentation:
 > https://firebase.google.com/docs/flutter/setup
```