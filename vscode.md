vscode remote develop
-------------------------------------------

- 确定VSCode客户端的commitid (vscode菜单->Help->about->commit:XXXXXXXX)
- 将${commit_id}替换为ea3859d4ba2f3e577a159bc91e3074c5d85c0523
<pre>
# Download vscode server from url: https://update.code.visualstudio.com/commit:${commit_id}/server-linux-x64/stable
# Upload the vscode-server-linux-x64.tar.gz to server
# Unzip the downloaded vscode-server-linux-x64.tar.gz to ~/.vscode-server/bin/${commit_id} without vscode-server-linux-x64 dir
# Create 0 file under ~/.vscode-server/bin/${commit_id}
</pre>

<pre>
# Download url is: https://update.code.visualstudio.com/commit:${commit_id}/server-linux-x64/stable
curl -sSL "https://update.code.visualstudio.com/commit:ea3859d4ba2f3e577a159bc91e3074c5d85c0523/server-linux-x64/stable" -o vscode-server-linux-x64.tar.gz

mkdir -p ~/.vscode-server/bin/ea3859d4ba2f3e577a159bc91e3074c5d85c0523
# assume that you upload vscode-server-linux-x64.tar.gz to /tmp dir
tar zxvf /tmp/vscode-server-linux-x64.tar.gz -C ~/.vscode-server/bin/ea3859d4ba2f3e577a159bc91e3074c5d85c0523--strip 1
touch ~/.vscode-server/bin/ea3859d4ba2f3e577a159bc91e3074c5d85c0523/0
</pre>




extensions
-------------------------------------------

|插件|描述|
|----|----|
|vim |vim模拟器|
|Draw.io |画流程图|
|Diff Folders |按目录进行比较|
|Doxygen Document Generator|生成注释|
|TextMaker(Highlighter) |对关键字进行着色|
|Partial Diff |比较部分内容|
|Text Power Tools |文本过滤|
|TODO Tree |查看todo列表|
|Bracket Pair Colorizer |括号颜色|
|Markdown All in One |编写MD|
|local history|查看本地文件修改历史|
|HexEditor |二进制编辑器，可按Hex进行搜索|
|Better Align |文本格式化（Ctrl+Shift+p输入“Align”）|
|change-case |修改大小写（Ctrl+Shift+p输入“change）|
