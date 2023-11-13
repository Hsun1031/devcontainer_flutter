FROM mcr.microsoft.com/devcontainers/base:ubuntu-22.04

# Flutter version
ENV FLUTTER_VERSION 3.13.9
ENV FLUTTER_CHANNEL stable

# Android commandlinetools version
ENV ANDROID_COMMANDTOOLS_VERSION 10406996

# Path
ENV HOME /home/vscode
ENV ANDROID_SDK_PATH $HOME/android-sdk
ENV CMDLINE_TOOLS_PATH $HOME/cmdline-tools/latest/bin
ENV FLUTTER_PATH $HOME/flutter/bin

USER vscode

# Install packages
RUN sudo apt-get update
RUN sudo apt-get -y install wget unzip openjdk-17-jdk
RUN sudo apt-get clean
RUN sudo rm -rf /var/lib/apt/lists/*

WORKDIR $HOME

# Download, unzip and remove Android commandlinetools and Flutter
RUN wget https://dl.google.com/android/repository/commandlinetools-linux-${ANDROID_COMMANDTOOLS_VERSION}_latest.zip
RUN wget https://storage.googleapis.com/flutter_infra_release/releases/stable/linux/flutter_linux_${FLUTTER_VERSION}-${FLUTTER_CHANNEL}.tar.xz

RUN unzip commandlinetools-linux-${ANDROID_COMMANDTOOLS_VERSION}_latest.zip
RUN tar xf flutter_linux_${FLUTTER_VERSION}-${FLUTTER_CHANNEL}.tar.xz

RUN rm commandlinetools-linux-${ANDROID_COMMANDTOOLS_VERSION}_latest.zip
RUN rm flutter_linux_${FLUTTER_VERSION}-${FLUTTER_CHANNEL}.tar.xz

# move cmdline-tools all data in cmdline-tools/latest
RUN mkdir cmdline-tools-latest
RUN mv cmdline-tools cmdline-tools-latest/latest
RUN mv cmdline-tools-latest cmdline-tools

# Settup Android SDK
RUN yes | ${CMDLINE_TOOLS_PATH}/sdkmanager --licenses --sdk_root=${ANDROID_SDK_PATH}
RUN mkdir ${ANDROID_SDK_PATH}

WORKDIR ${ANDROID_SDK_PATH}

RUN ${CMDLINE_TOOLS_PATH}/sdkmanager --install "cmdline-tools;latest" --sdk_root=${ANDROID_SDK_PATH}
RUN ${CMDLINE_TOOLS_PATH}/sdkmanager "platform-tools" --sdk_root=${ANDROID_SDK_PATH}

# Settup Android Flutter
WORKDIR /home/vscode

RUN ${FLUTTER_PATH}/flutter config --android-sdk ${ANDROID_SDK_PATH}
RUN ${FLUTTER_PATH}/flutter doctor

RUN echo 'export PATH="$PATH:${CMDLINE_TOOLS_PATH}"' >> ${HOME}/.bashrc
RUN echo 'export PATH="$PATH:${FLUTTER_PATH}"' >> ${HOME}/.bashrc
