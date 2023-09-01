Open NGROK
Sign up in NGROK and verify your account if you're signed up using e-mail, and after that go back to github and create a new repository make it private if you want (recommended), and after create it then go to actions and click on set up a workflow yourself  and after that go to settings and click on Secrets and variables and click on Actions, after that click on New repository secret and in the name type the

NGROK AUTH_
NGROK_AUTH_TOKEN
NGROK_AUTH_TOKEN and in Secret type the Your NGROK AuthToken you can find it if you go back to NGROK an click on Getting Started and click on Your AuthToken and copy the code and paste it in *Secret in Github and click Add secret, after adding the secret go to actions again and now you will see Simple Workflow click on Configure and remove the old code and replace it with that code:

RDP Configure Yaml Code
name: CI


on: [push, workflow_dispatch]


jobs:

  build:


    runs-on: windows-latest


    steps:

    - name: Download

      run: Invoke-WebRequest https://bin.equinox.io/c/4VmDzA7iaHb/ngrok-stable-windows-amd64.zip -OutFile ngrok.zip

    - name: Extract

      run: Expand-Archive ngrok.zip

    - name: Auth

      run: .\ngrok\ngrok.exe authtoken $Env:NGROK_AUTH_TOKEN

      env:

        NGROK_AUTH_TOKEN: ${{ secrets.NGROK_AUTH_TOKEN }}

    - name: Enable TS

      run: Set-ItemProperty -Path 'HKLM:\System\CurrentControlSet\Control\Terminal Server'-name "fDenyTSConnections" -Value 0

    - run: Enable-NetFirewallRule -DisplayGroup "Remote Desktop"

    - run: Set-ItemProperty -Path 'HKLM:\System\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp' -name "UserAuthentication" -Value 1

    - run: Set-LocalUser -Name "runneradmin" -Password (ConvertTo-SecureString -AsPlainText "P@ssw0rd!" -Force)

    - name: Create Tunnel

      run: .\ngrok\ngrok.exe tcp 3389

Copy the code and replace it with the old code

paste it here

And click on Commit changes

z

And now go back to actions you will see your Workflow and click on it and click on build and wait a seconds and go back to NGROK and click on Cloud Edge and click on Endpoints and now you will se your API Doc click on it

API Doc

And copy the URL after top:// like this:

Copy it

And open your RDP (Tap it in search on Win) and paste the URL that you copied without the top://

RDP - Remote Desktop Protocol

And in Username type this username :

Username
runneradmin
And in the Password type this password

Password
P@ssw0rd!
And That's it!!

RDP Lifetime

Hope that helps You all :)
