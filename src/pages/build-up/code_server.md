# Spin-up your own VS Code Server instance in Build

<iframe width="373" height="663" src="https://www.youtube.com/embed/2QDsyR0kvo0" title="VS Code Server on iPad in 59 seconds" frameBorder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

## References
[The Visual Studio Code Server](https://code.visualstudio.com/blogs/2022/07/07/vscode-server)

## Comments
With Blink Build, you can have your private VS Code Server instance in just seconds, accessible on demand from your iPad or iPhone. Participate in our [discussion](https://github.com/blinksh/blink/discussions/1727) to make the most out of it!

## Troubleshooting
- If VS Code is not loading at all or it is showing a blank screen. Try closing the tab and starting `code` again. Also try closing Blink and reopening it. 
- Make sure the Blink-FS extension is installed and Enabled. [Reference.](https://github.com/blinksh/blink/issues/1304)
- If you have issues enabling Blink-FS, or getting the extensions to come through, https://vscode.dev may be having problems. In those cases, we have seen that changing to the Nightly version may work, as suggested in this [Discussion](https://github.com/blinksh/blink/discussions/1795#discussioncomment-6262467).
- Make sure SFTP is enabled in the remote, and that authentication requires no user input (like passwords or 2FA). One good test for this is to [enable the Files.app integration](https://docs.blink.sh/advanced/files-app) and browsing files there. [Refrence.](https://github.com/blinksh/blink/issues/1880)
- Make sure your remote path is valid. Try accessing your home folder with `code <host>:~/`. Then try using the Files.app integration, navigate to the folder you want to work on, long tap on it and `Open in Code`, this will automatically complete the paths for you and will allow you to see how it is accessed in the remote. 
- Check logs. `~/.blink/blinkCode.log`. This may give you a clue of where things stopped.
- Send a support request with the logs to Discussions.
