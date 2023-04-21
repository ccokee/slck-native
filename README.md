# SLCK Vue-Native Terminal App

The SLCK Vue-Native Terminal App is a mobile application built using Vue-Native and integrated with the SLCK system. This app provides a secure terminal environment for running commands on a remote SLCK backend, allowing users to interact with command-line applications through a simple and intuitive interface.

## Prerequisites

Before you begin, make sure you have the following installed:

1. [Node.js](https://nodejs.org/en/download/) (version 12.x or later)
2. [Expo CLI](https://docs.expo.dev/get-started/installation/) (version 4.x or later)
3. [Vue Native CLI](https://vue-native.io/docs/installation.html) (version 2.x or later)

## Setup

1. Clone the SLCK Vue-Native Terminal App repository:

   ```sh
   git clone https://github.com/ccokee/slck-vue-native-terminal.git
   cd slck-vue-native-terminal
   ```

2. Install the required dependencies:

   ```sh
   npm install
   ```

3. Start the development server:

   ```sh
   expo start
   ```

4. Open the Expo app on your iOS or Android device and scan the QR code displayed in the terminal or browser window.

## Build

To build the app for production, follow these steps:

1. Build the standalone app for iOS or Android:

   ```sh
   expo build:android
   ```

   or

   ```sh
   expo build:ios
   ```

   This will generate an APK or IPA file, respectively, which can be distributed and installed on compatible devices.

2. Download the build files from the URL provided by Expo after the build process is complete.

## Configuration

To connect the SLCK Vue-Native Terminal App to your SLCK backend, update the `SLCK_BACKEND_URL` variable in the `config.js` file:

```javascript
export const SLCK_BACKEND_URL = 'https://your-slck-backend-url.com';
```

Replace `'https://your-slck-backend-url.com'` with the actual URL of your SLCK backend.

## Usage

Once the app is running on your device, you can use the terminal interface to interact with the SLCK backend:

1. Type a command in the input field at the bottom of the screen.
2. Press the "Enter" key on your device's keyboard to send the command to the SLCK backend.
3. The command's output will be displayed in the terminal window above the input field.

## Contributing

We welcome contributions to the SLCK Vue-Native Terminal App project! If you'd like to contribute, please follow the standard GitHub workflow: fork the repository, create a new branch, make your changes, and submit a pull request. Make sure to follow the existing code style and provide clear, concise commit messages.

## License

Copyright 2023.

Licensed under the MIT License (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    https://opensource.org/licenses/MIT

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
