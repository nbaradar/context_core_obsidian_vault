# VS Code/WSL Integration

###### Enable Hyper-V
- Open the Windows Start Menu and search for "Turn Windows features on or off."
- In the list of features, scroll down and find "Hyper-V."
- Check the box next to "Hyper-V" and any subfeatures it might have.
- Click "OK" and follow any on-screen prompts to complete the installation.
- **Restart your computer** for the changes to take effect.
###### Install WSL
Open powershell as admin, run this command:
`wsl --install`
###### Install VSCode Remote
This is a WSL extension.  Launch VSCode, go to Extensions view (Ctrl+Shift+X) and get the [WSL Extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-wsl)
