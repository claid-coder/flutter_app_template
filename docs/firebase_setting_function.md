# Firebase function deploy by CLI

https://firebase.google.com/docs/cli?hl=ko#install-cli-mac-linux

```shell
$ cd functions
$ npm install firebase-functions@latest

functions % npm install firebase-functions@latest
npm warn EBADENGINE Unsupported engine {
npm warn EBADENGINE   package: undefined,
npm warn EBADENGINE   required: { node: '18' },
npm warn EBADENGINE   current: { node: 'v22.13.1', npm: '11.1.0' }
npm warn EBADENGINE }

added 1 package, removed 2 packages, changed 3 packages, and audited 529 packages in 4s

57 packages are looking for funding
run `npm fund` for details

4 critical severity vulnerabilities

To address all issues (including breaking changes), run:
npm audit fix --force

Run `npm audit` for details.
```

Node.js 버전 충돌 문제가 있네요. Firebase Functions는 Node.js 18을 요구하는데 현재 v22가 설치되어 있습니다.
nvm을 사용하여 Node.js 버전을 변경하겠습니다:

```shell
# Node.js 18 설치
$ nvm install 18

# Node.js 18로 전환
$ nvm use 18

# functions 디렉토리로 이동
$ cd functions

# 패키지 재설치
$ npm install firebase-functions@latest
```

```shell
$ npm install firebase-admin@^13.0.2
zsh: no matches found: firebase-admin@^13.0.2
$ firebase deploy --only functions

=== Deploying to 'copy-voice-chat'...

i  deploying functions
i  functions: preparing codebase default for deployment
i  functions: ensuring required API cloudfunctions.googleapis.com is enabled...
i  functions: ensuring required API cloudbuild.googleapis.com is enabled...
i  artifactregistry: ensuring required API artifactregistry.googleapis.com is enabled...
⚠  artifactregistry: missing required API artifactregistry.googleapis.com. Enabling now...
⚠  functions: missing required API cloudbuild.googleapis.com. Enabling now...
✔  functions: required API cloudfunctions.googleapis.com is enabled
✔  artifactregistry: required API artifactregistry.googleapis.com is enabled
✔  functions: required API cloudbuild.googleapis.com is enabled
i  functions: Loading and analyzing source code for codebase default to determine what to deploy
Serving at port 8974

Error: Failed to parse build specification:
- FirebaseError Unexpected key extensions. You may need to install a newer version of the Firebase CLI.
```

이 명령어는 Firebase CLI를 전역(global)으로 설치하거나 업데이트합니다. 설치 또는 업데이트 후, 다음 명령어로 버전이 최신으로 업데이트되었는지 확인합니다:

```shell
% firebase --version

13.2.1

   ╭─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╮
   │                                                                                                                     │
   │                                          Update available 13.2.1 → 13.29.3                                          │
   │                                   To update to the latest version using npm, run                                    │
   │                                            npm install -g firebase-tools                                            │
   │   For other CLI management options, visit the CLI documentation (https://firebase.google.com/docs/cli#update-cli)   │
   │                                                                                                                     │
   │                                                                                                                     │
   │                                                                                                                     │
   ╰─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯

//% npm uninstall -g firebase-tools
//% npm cache clean --force
//% npm install -g firebase-tools
$ npm install -g firebase-tools@latest

added 634 packages in 18s

70 packages are looking for funding
  run `npm fund` for details

% firebase --version
13.2.1 → 버전 업데이트가 안 되는데???
쉘(bash, zsh) 자체를 재시작 할 것
```

```shell
% firebase deploy --only functions
(node:89291) [DEP0040] DeprecationWarning: The `punycode` module is deprecated. Please use a userland alternative instead.
(Use `node --trace-deprecation ...` to show where the warning was created)

=== Deploying to 'copy-voice-chat'...

i  deploying functions
i  functions: preparing codebase default for deployment
i  functions: ensuring required API cloudfunctions.googleapis.com is enabled...
i  functions: ensuring required API cloudbuild.googleapis.com is enabled...
i  artifactregistry: ensuring required API artifactregistry.googleapis.com is enabled...
✔  functions: required API cloudfunctions.googleapis.com is enabled
✔  artifactregistry: required API artifactregistry.googleapis.com is enabled
✔  functions: required API cloudbuild.googleapis.com is enabled
⚠  functions: Runtime Node.js 18 will be deprecated on 2025-04-30 and will be decommissioned on 2025-10-31, after which you will not be able to deploy without upgrading. Consider upgrading now to avoid disruption. See https://cloud.google.com/functions/docs/runtime-support for full details on the lifecycle policy
i  functions: Loading and analyzing source code for codebase default to determine what to deploy
Serving at port 8155

(node:89311) [DEP0040] DeprecationWarning: The `punycode` module is deprecated. Please use a userland alternative instead.
(Use `node --trace-deprecation ...` to show where the warning was created)

i  extensions: ensuring required API firebaseextensions.googleapis.com is enabled...
⚠  extensions: missing required API firebaseextensions.googleapis.com. Enabling now...
✔  extensions: required API firebaseextensions.googleapis.com is enabled
i  functions: Loaded environment variables from .env.
i  functions: cleaning up build files...

✔  Deploy complete!

Project Console: https://console.firebase.google.com/project/copy-voice-chat/overview
```

배포 전 필요한 추가 설정:

1. package.json에 OpenAI 패키지 추가:

```shell
% cd functions
% npm install openai
npm warn EBADENGINE Unsupported engine {
npm warn EBADENGINE   package: undefined,
npm warn EBADENGINE   required: { node: '18' },
npm warn EBADENGINE   current: { node: 'v22.13.1', npm: '11.1.0' }
npm warn EBADENGINE }
npm warn deprecated google-p12-pem@4.0.1: Package is no longer maintained
npm warn deprecated glob@8.1.0: Glob versions prior to v9 are no longer supported

added 75 packages, removed 17 packages, changed 29 packages, and audited 544 packages in 7s

58 packages are looking for funding
  run `npm fund` for details

4 critical severity vulnerabilities

To address all issues (including breaking changes), run:
  npm audit fix --force

Run `npm audit` for details.
```

2. dotenv 패키지를 설치합니다:
```shell
% npm install dotenv
npm warn EBADENGINE Unsupported engine {
npm warn EBADENGINE   package: undefined,
npm warn EBADENGINE   required: { node: '18' },
npm warn EBADENGINE   current: { node: 'v22.13.1', npm: '11.1.0' }
npm warn EBADENGINE }

added 1 package, and audited 545 packages in 1s

59 packages are looking for funding
  run `npm fund` for details

4 critical severity vulnerabilities

To address all issues (including breaking changes), run:
  npm audit fix --force

Run `npm audit` for details.
```

프로젝트를 위한 추가 패키지

```shell
npm install busboy
```

3. Firebase Secret 설정:
프로덕션 환경에서는 여전히 Firebase Secret을 사용
```shell
% firebase functions:secrets:set OPENAI_API_KEY
(node:92570) [DEP0040] DeprecationWarning: The `punycode` module is deprecated. Please use a userland alternative instead.
(Use `node --trace-deprecation ...` to show where the warning was created)
? Enter a value for OPENAI_API_KEY [input is hidden]
이걸로는 안 해봄
```

---

## Deploy

```shell
% firebase deploy --only functions
(node:94009) [DEP0040] DeprecationWarning: The `punycode` module is deprecated. Please use a userland alternative instead.
(Use `node --trace-deprecation ...` to show where the warning was created)

=== Deploying to 'copy-voice-chat'...

i  deploying functions
i  functions: preparing codebase default for deployment
i  functions: ensuring required API cloudfunctions.googleapis.com is enabled...
i  functions: ensuring required API cloudbuild.googleapis.com is enabled...
i  artifactregistry: ensuring required API artifactregistry.googleapis.com is enabled...
✔  functions: required API cloudbuild.googleapis.com is enabled
✔  artifactregistry: required API artifactregistry.googleapis.com is enabled
✔  functions: required API cloudfunctions.googleapis.com is enabled
⚠  functions: Runtime Node.js 18 will be deprecated on 2025-04-30 and will be decommissioned on 2025-10-31, after which you will not be able to deploy without upgrading. Consider upgrading now to avoid disruption. See https://cloud.google.com/functions/docs/runtime-support for full details on the lifecycle policy
⚠  functions: package.json indicates an outdated version of firebase-functions. Please upgrade using npm install --save firebase-functions@latest in your functions directory.
⚠  functions: Please note that there will be breaking changes when you upgrade.
i  functions: Loading and analyzing source code for codebase default to determine what to deploy
i  functions: You are using a version of firebase-functions SDK (4.9.0) that does not have support for the newest Firebase Extensions features. Please update firebase-functions SDK to >=5.1.0 to use them correctly
Serving at port 8107

(node:94038) [DEP0040] DeprecationWarning: The `punycode` module is deprecated. Please use a userland alternative instead.
(Use `node --trace-deprecation ...` to show where the warning was created)

i  functions: Loaded environment variables from .env.
i  functions: preparing functions directory for uploading...
i  functions: packaged /Users/[username]/Workspace/CursorStudy/copy_voice_chat/functions (71.44 KB) for uploading
✔  functions: functions folder uploaded successfully
i  functions: creating Node.js 18 (1st Gen) function textToSpeech(asia-northeast3)...
✔  functions[textToSpeech(asia-northeast3)] Successful create operation.
Function URL (textToSpeech(asia-northeast3)): https://asia-northeast3-copy-voice-chat.cloudfunctions.net/textToSpeech
i  functions: cleaning up build files...
⚠  functions: Unhandled error cleaning up build images. This could result in a small monthly bill if not corrected. You can attempt to delete these images by redeploying or you can delete them manually at https://console.cloud.google.com/gcr/images/copy-voice-chat/asia/gcf

✔  Deploy complete!

Project Console: https://console.firebase.google.com/project/copy-voice-chat/overview
```

Function URL 뒤에 주소 있음