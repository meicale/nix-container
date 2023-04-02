# Portable & Personal Development Environment 
#
# Copyright (C) 2022-2023  Bill King

# P2开发环境

## 技术要求
* docker 容器，使用该开发环境仅依赖 docker 容器，所有的依赖和工具等均需要安装在容器中，并在容器中运行。项目相关的依赖需要在dev 容器中进行配置。
* NeoVim：以Neovim为主配置相应的开发环境，配套相应的插件和插件所需的bin等内容。
* CLI 工具：进阶的linux 命令行工具。比如：rg，ranger等。
* nix（optional）：为了更方便的 适配不同的开发环境的需求，可以根据不同的项目进行切换和实验，需要nix提供脚本化的支持，并请方便进行实验。

## 希望的特性
* 开箱即用，支持多种开发环境的配置。仅需依赖与docker，代码进行映射或者ssh到服务器，就可以开始工作。
* TUI支持：：支持以terminal与multi-pluxer兼容的开发环境，在集中的环境中完成绝大部分工作。
* 全面支持remote核心功能：比如，执行命令和脚本，debug，lsp，neotest等，并能够接近neovim本地的原生体验。
* 图形界面（optional）：支持NeoVide，VSCode等图形界面，并以WLS模型在Windows系统下运行，和Tiling Windows 软件兼容。

## 开发计划
- [] neovim 基础配置
  - [x] 基于git@github.com:meicale/Neovim-from-scratch.git，原生的neovim配置
  - [x] 核心：跳转的配置，移动的配置
  - [] optional, 使用docker 容器配置的通用的neovim mini版本，详见dockerfile_minimal，将包括lazyvim等配置为项目的submoduel。考虑到需要调整部分的代码，使用相应的fork版本。
- [] nixpkg 的支持
  - [] 基于nix对neovim进行配置
  - [] git@github.com:meicale/.nix_dotfiles.git 目前不太容易配置，原因包括网络不稳定等，nixpkg中的包更新很难。
- [] remote 支持
  - [x] dev container 脚本运行。使用nvim asynctask 并配置justfile实现程序的运行。基于目录映射的脚本，实现结果的替换，并输入到quickfix中
  - [x] remote dap 实现程序的debug。debugpy 及相应的dap的配置目前已经支持。
  - [] remote lsp 支持，目前使用distant.nvim 方案，在dev-container环境出现bug，待作者反馈。
  - [] remote neotest 支持，目前python相关的config 比较复杂，待作者反馈。
- [] 键统一配置
  - [] 架构与层次:三层架构，基础为OS上的Tiling Windows Manager（比如awesome 等），终端模拟器上的复用工具（比如zellij等），终端中的modual编辑器（比如neovim等）


## 主要结果
