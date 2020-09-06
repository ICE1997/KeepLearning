# Iterm2使用记录

## 基本软件安装（前提已安装brew）

```bash
brew cask install iterm2 ##安装Iterm2
```

```bash
brew install zsh ##安装zsh
```

## zsh配置文件 oh-my-zsh安装

```bash
$ sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)" ##下载并安装oh-my-zsh
```

## Iterm2美化

### 更改配色方案

```bash
curl -O https://raw.githubusercontent.com/MartinSeeler/iterm2-material-design/master/material-design-colors.itermcolors ##下载material配色方案
```

1. 打开 *iTerm2 > Preferences > Profiles > Colors Tab*

2. 在最底部点击 *Color Presets…* 

3. 点击 *Import…*

4. 选择 `material-design-colors.itermcolors` 文件

5. 从*Load Presets…*选择 *material-design-colors*  
6. 下载[Meslo字体](https://github.com/powerline/fonts/blob/master/Meslo%20Slashed/Meslo%20LG%20M%20Regular%20for%20Powerline.ttf)
7. 安装字体到系统字体册
8. 在iTerm2中应用字体 iTerm -> Preferences -> Profiles -> Text -> Change Font）

## 命令提示与补全

1. 克隆仓库到本地 ~/.oh-my-zsh/custom/plugins 路径下

```bash
git clone git://github.com/zsh-users/zsh-autosuggestions $ZSH_CUSTOM/plugins/zsh-autosuggestions
```

2. 用 vim 编辑 .zshrc 文件，找到插件设置命令，默认是 `plugins=(git)` ，把它修改为`plugins=(zsh-autosuggestions git)`

## 语法高亮效果

```bash
brew install zsh-syntax-highlighting ##安装zsh-syntax-highlighting
```

```bash
source /xxx/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh ##添加在.zhsrc最后一行
```

## 更多

1. iTerm2 默认使用dash改用zsh解决方法：`chsh -s /bin/zsh`
2. iTerm2 zsh切换回原来的dash：`chsh -s /bin/bash`
3. 卸载`oh my zsh`，在命令行输入：`uninstall_oh_my_zsh`
