# Ghostty

[ghostty官网](https://ghostty.org/)

## 安装和更新

### Mac

```shell
# 安装ghostty
brew install --cask ghostty

# 升级ghostty
brew upgrade --cask ghostty

# 查看ghostty版本
ghostty +version
```

### Ubuntu

```shell
sudo snap install ghostty --classic
```

## 快捷键

### Mac

```shell
# 查看快捷键
ghostty +list-keybinds --default

# 左右分屏
⌘ + D

# 上下分屏
⌘ + Shift + D

# 切换分屏
⌘ + [
⌘ + ]
⌘ + alt + arrow_up
⌘ + alt + arrow_down
⌘ + alt + arrow_left
⌘ + alt + arrow_right

# 关闭当前分屏
⌘ + W
```

## 外观

### Mac/Ubuntu

```shell
# 查看并预览内置主题
ghostty +list-themes

# 修改配置文件
mkdir -p ~/.config/ghostty
vim ~/.config/ghostty/config

# 修改主题
theme = Catppuccin Mocha
window-theme = ghostty

# 修改透明度
background-opacity = 0.8
# 毛玻璃效果
background-blur-radius = 3

```

# Starship

Starship 是跨平台提示符工具

## 安装

### Mac


```shell
brew install starship
starship --version

starship preset catppuccin-powerline -o ~/.config/starship.toml
echo 'eval "$(starship init zsh)"' >> ~/.zshrc

source ~/.zshrc
```

### Ubuntu

```shell

curl -sS [https://starship.rs/install.sh](https://starship.rs/install.sh) | sh
starship --version

starship preset catppuccin-powerline -o ~/.config/starship.toml
echo 'eval "$(starship init bash)"' >> ~/.bashrc

source ~/.bashrc
```
