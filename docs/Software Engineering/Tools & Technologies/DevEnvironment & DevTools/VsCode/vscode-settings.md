## Ignore whitespace in Visual Studio Code git diff view

how to avoid whitespace changes in vscode source control

Solution:

Add this in User => Settings.json (CTRL+SHIFT+P)

```jsx showLineNumbers
// Add on your settings.json:
"diffEditor.ignoreTrimWhitespace": true,
```

https://stackoverflow.com/questions/40779222/ignore-whitespace-in-visual-studio-code-git-diff-view#:~:text=It's%20also%20available%20in%20Preferences%2CSettings.&text=File%20%3D%3E%20Preferences%20%3D%3E%20Settings,Editor%20%3D%3E%20Ignore%20Trim%20Whitespace.
