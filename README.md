<h1>GUIA DE INSTALAÇÃO MAESTRO WINDOWS</h1> 

<h2>Este documento serve de guia simplificado e direto para instalação do Maestro em ambiente Windows</h2>

<h1>Pré-Requesitos</h1>

1.PowerShell instalado no seu Sistema Windows.
2.Android Studio Instalado na sua maquina Windows.
3.Adicionar ANDROID_HOME nas variaveis de sistema Windows.
-- Verificar se ANDROID_HOME está sendo chamado pelo sistema, abra o PowerShell e rode esse comando adb --version.
-- note a versão do ADB.
4.Java JDK 11 instalado e variavel JAVA_HOME configurada.
-- Verificar se java esásendo chamado pelo sistema windows, no terminal rode comando java --version para checar se está funcionando.

 _____________________________________________________
|                                                     |
# Passo 1 - Instalar WSL                              |
|_____________________________________________________|

abra terminal windows e rode esse comando
wsl --install -d Ubuntu
REMOVER
wsl -l -v          //lista nome
wsl --unregister Ubuntu-22.04

 _____________________________________________________
|                                                     |
# Passo 2 - Configurar Linux WSL                      |
|_____________________________________________________|

sudo apt update
sudo apt -y upgrade
sudo apt -y install openjdk-11-jdk
curl -Ls "https://get.maestro.mobile.dev" | bash
sudo apt -y install unzip
sudo apt -y install sdkmanager
sudo apt -y install adb

## Step 1: Create and navigate to the Android directory
mkdir ~/Android
cd ~/Android

## Step 2: Download Android Command Line Tools ZIP file
wget https://dl.google.com/android/repository/commandlinetools-linux-6858069_latest.zip

## Step 3: Unzip the ANdroid Command Line Tools ZIP file
unzip commandlinetools-linux-6858069_latest.zip

## Step 4: Create the tools directory and move the files
mkdir tools
mv cmdline-tools/* tools/

## step 5: add envoroment variables to ~/.bashrc

echo 'export ANDROID_HOME=$HOME/Android' >> ~/.bashrc
echo 'export PATH=$PATH:$ANDROID_HOME/tools/bin/:$PATH' >> ~/.bashrc
echo 'export ANDROID_SDK_ROOT=$HOME/Android' >> ~/.bashrc

## step 6: Reload ~/.bashrc
source ~/.bashrc

## step 7: Install Platform tools
sdkmanager --install "platform-tools"

## step 8:add Platform tools to ~/.bashrc
echo 'export PATH=$PATH:$ANDROID_HOME/platform-tools/:$PATH' >> ~/.bashrc

## step 9: Reload ~/.bashrc
source ~/.bashrc

## step 10: Close and relaunch terminal
## (this step needs to be done manually) 
## !/bin/bash

 _____________________________________________________
|                                                     |
# Passo 3 - SUBIR SERVER ADB                          |
|_____________________________________________________|

## no terminal windows 
adb -a -P 5037 nodaemon server

adb kill-server                      //matar server

## no terminal LINUX
export ADB_SERVER_SOCKET=tcp:172.108.6.125:5037
adb kill-server                      //para matar server

verificar se está conectado
adb devices

mastro --host 172.108.6.125 test android-flow.yaml

mastro --host 172.108.6.125 test android-flow.yaml

mastro --host 172.108.6.125 test .subflows/sub.yaml

mastro --host 172.108.6.125 studio        //inspector ---  http://localhost:9999/interact

 _____________________________________________________
|                                                     |
# Passo 4 - Testar Maestro                            |
|_____________________________________________________|

com.qazandoqafood

- tapOn:
- inpuutText:
- assertVisible:
	id:"email"
- assertVisible: "E-mail"





