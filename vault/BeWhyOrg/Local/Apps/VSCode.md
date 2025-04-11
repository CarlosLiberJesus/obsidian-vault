# Install

I like to manually set in the apt repository, it ensures the regular update, when we update the system:

```bash
sudo apt-get install wget gpg
wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > packages.microsoft.gpg
sudo install -D -o root -g root -m 644 packages.microsoft.gpg /etc/apt/keyrings/packages.microsoft.gpg
echo "deb [arch=amd64,arm64,armhf signed-by=/etc/apt/keyrings/packages.microsoft.gpg] https://packages.microsoft.com/repos/code stable main" |sudo tee /etc/apt/sources.list.d/vscode.list > /dev/null
rm -f packages.microsoft.gpg
```

## Config and Extension

Learning is a spiral process that we don't get it right at first! In this new cycles we use profiles to host different packages. This is ensure or AI agents are not running all in the same workspace, so we can switch profiles and have access to optimized Agents like:

- [[Cline]] 
- [[Qodo]]
- [[Augment]]
- we might add more, we still have the weak fully free copilot until the end of year

Each of this agents have their strengths, so we can switch between then without collisions. You can still use the Default Profile the install commum Extensions and then copy them to the "AI profiles"

## plugins:
- [generic movie](https://www.youtube.com/watch?v=lxRAj1Gijic)
- [drawio](https://marketplace.visualstudio.com/items?itemName=hediet.vscode-drawio)
- [code diagram](https://www.codediagram.io/)
