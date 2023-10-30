# Use the Microsoft dev container as the base image
# FROM mcr.microsoft.com/vscode/devcontainers/universal
FROM mcr.microsoft.com/openjdk/jdk:11-ubuntu

# Set environment variables used by the Android SDK
# ENV ANDROID_SDK_HOME /opt/android-sdk-linux
# ENV ANDROID_SDK_ROOT /opt/android-sdk-linux
# ENV ANDROID_HOME /opt/android-sdk-linux
# ENV ANDROID_SDK /opt/android-sdk-linux

# Set Debian to not prompt for user input during package installation
ENV DEBIAN_FRONTEND noninteractive

# Update package list and install packages required for Android app development
RUN apt-get update -yqq && \
    apt-get install -y \
      curl \
      expect \
      git \
      make \
      wget \
      unzip \
      vim \
      openssh-client \
      locales \
      libarchive-tools && \
    apt-get clean && rm -rf /var/lib/apt/lists/* && \
    localedef -i en_US -c -f UTF-8 -A /usr/share/locale/locale.alias en_US.UTF-8

RUN wget https://download.visualstudio.microsoft.com/download/pr/61f29db0-10a5-4816-8fd8-ca2f71beaea3/e15fb7288eb5bc0053b91ea7b0bfd580/dotnet-sdk-7.0.401-linux-x64.tar.gz && \
    mkdir -p $HOME/dotnet && tar zxf dotnet-sdk-7.0.401-linux-x64.tar.gz -C $HOME/dotnet

# dotnet exports
RUN echo 'export DOTNET_ROOT=$HOME/dotnet' >> ~/.bashrc
RUN echo 'export PATH=$PATH:$HOME/dotnet' >> ~/.bashrc


# RUN wget https://dotnet.microsoft.com/download/dotnet/scripts/v1/dotnet-install.sh && \
#     chmod +x dotnet-install.sh && \
#     dotnet-install.sh

# RUN echo 'export DOTNET_ROOT=$HOME/.dotnet' >> ~/.bashrc
# RUN echo 'export PATH=$PATH:$HOME/.dotnet' >> ~/.bashrc

    
# Android SDK
# RUN wget http://dl.google.com/android/repository/commandlinetools-linux-10406996_latest.zip
# RUN mkdir /opt/android-sdk-linux
# RUN unzip commandlinetools-linux-10406996_latest -d /opt/android-sdk-linux
# RUN mv /opt/android-sdk-linux/cmdline-tools/ /opt/android-sdk-linux/tools/

# Found this version of the CommandLineTools here https://stackoverflow.com/questions/42912824/the-ant-folder-is-suddenly-missing-from-android-sdk-did-google-remove-it
RUN wget https://dl.google.com/android/repository/tools_r25.2.5-linux.zip
RUN mkdir /opt/android-sdk-linux
RUN unzip tools_r25.2.5-linux.zip -d /opt/android-sdk-linux


# Android exports
RUN echo 'export ANDROID_HOME=/opt/android-sdk-linux' >> ~/.bashrc
RUN echo 'export PATH=$PATH:$ANDROID_HOME/tools:$ANDROID_HOME/tools/bin:$ANDROID_HOME/platform-tools' >> ~/.bashrc

# RUN cd /workspaces/AndroidSdkTestBed/ && dotnet workload install android
# RUN cd /workspaces/AndroidSdkTestBed/ && dotnet tool install -g Redth.Net.Maui.Check

# Set the system language to US English
ENV LANG en_US.UTF-8

# Create a new group and user with UID 1001
RUN groupadd android && \
    useradd -d /opt/android-sdk-linux -g android -u 1001 android

# Copy the tools and licenses directories to the /opt directory in the image
# COPY tools /opt/tools
# COPY licenses /opt/licenses

# Set the working directory to /opt/android-sdk-linux and run the entrypoint script
# WORKDIR /opt/android-sdk-linux
# RUN /opt/tools/entrypoint.sh built-in
