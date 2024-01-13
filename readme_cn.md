# Portable & Personal Development Environment 
# P2Dev

# Copyright (C) 2022-2023  Bill King

# P2开发环境

## 技术要求
* docker 容器，使用该开发环境仅依赖 docker 容器，所有的依赖和工具等均需要安装在容器中，并在容器中运行。项目相关的依赖需要在dev 容器中进行配置。
* NeoVim：以Neovim为主配置相应的开发环境，配套相应的插件和插件所需的bin等内容。
* CLI 工具：进阶的linux 命令行工具。比如：rg，ranger等。
* nix/home-manager：
为了更方便的适配不同的开发环境的需求，可以根据不同的项目进行切换和实验，需要nix提供脚本化的支持，并请方便进行实验。(TODO: dev-box)

## 希望的特性
* 开箱即用，支持多种开发环境的配置。仅需依赖docker，代码进行映射或者ssh到服务器，就可以开始工作。
* TUI支持：：支持以terminal与multi-pluxer兼容的开发环境，在集中的环境中完成绝大部分工作。
* 全面支持remote核心功能（optional）：比如，执行命令和脚本，debug，lsp，neotest等，并能够接近neovim本地的原生体验。使用VSCode作为远程的前端。
neovimconf2023 中后面会添加vscode-remote 类似的功能，所有，二者的结合部分不用花费太多精力。
* 图形界面（optional）：支持NeoVide，VSCode等图形界面，并以WLS模型在Windows系统下运行，和Tiling Windows 软件兼容。
* 键统一配置
  - [] 架构与层次:三层架构，基础为OS上的Tiling Windows Manager（比如awesome 等），终端模拟器（alertty或wezterm）上的复用工具（比如zellij等），终端中的modual编辑器（比如neovim等）
  - [] keys的配置：可配置的键盘（input-method驱动和keychron等键盘）：配置主要使用home row的五排键盘，小拇指和大拇指能方便的配置不同的modekey，ahk2 配置Windows 系统级键盘：通用的字符替换比如pw等，终端和复用器：简要配置复制/黏贴等关键快捷键和窗口操作键，编辑器配置：vscode中的组合键nvim中编辑chord键
  - [] 键位： 类似的动作使用类似的键位配置但是可以添加不同的mode-key。
    - [] 移动光标    
      - [] 标签的页的移动
      - [] 光标的到不同的”分区“
      - [] 不同的tag 之间的移动
    - [] vscode 和 nvim（optional)
      - [] 跳转到定义，引用，和跳回
      - [] explore的打开和关闭，跳转到文件（enter），增删重命名
      - [] 终端的打开，关闭，移动和相互跳转
      - [] debug, 端点，开启，继续执行到下一个断点，跳过，进入，终止
      - [] 自动测试相关，所有，文件，最近，上一个，进入debug
* 配置化可移植的系统
  - [] 系统层和项目层可以分开，所有的配置配置基于git仓库完成，并实现一键复现。
  - [] 模块化的系统，基于Linux系统命令行工具，编辑器和终端复用的一个核心。
* AI 支持的交互
  - [] AI辅助代码编写，在vscode端（copilot，codium）neovim端（chatgpt，codium)
  - [] AI辅助文档的处理，需要本地的llm的支持，也可以用来处理代码。
  - [] 智能的交互方法。包括语音输入与控制（copilot voice, Cursorless 编程和laton voice语音命令），眼球跟踪待调研。
  - [] 智能终端warp等，需要在Windows上支持之后尝试。
* 私有AI支持
  - [] ollama，更方便的本地/私有模型的部署，可以方便的部署和组合模型的能力。
  - [] 支持的模型，codeshell，chatglm，ollama，等，实现的功能包括编程、写作等场景的支持。
  - [] 支持的框架，gen.nvim, ChatGPT.nvim，academic.nvim 等支持，整合对应的能力，并拓展相应的框架，集中到nvim等编辑器界面，也可以浏览器中实现，可以转移到类似vscode中进行实现。
  - [] 共有的也应该支持，比如openai等的api这样的工具，但是，这种方法相对简单，应该不需要太多的配置就能实现。

## 开发计划
- [] neovim 基础配置
  - [x] 基于git@github.com:meicale/Neovim-from-scratch.git，原生的neovim配置
  - [x] 核心：跳转的配置，移动的配置，包括通用的hup，leap和flash等插件的结合使用，在“视野内” 的跳转达到非常高的效率。实现“*五键一秒*”到达页面内任何位置。
  - [] optional, 使用docker 容器配置的通用的neovim mini版本，详见dockerfile_minimal，将包括lazyvim等配置为项目的submoduel。考虑到需要调整部分的代码，使用相应的fork版本。
- [] nix 可完整复用的支持
  - [] 基于nix对neovim进行配置，使用nixvim实现基础版，使用xdg等nix工具，配置比较完整的发行版比如，lazyvim和lunarvim。
  - [x] git@github.com:meicale/.nix_dotfiles.git 目前不太容易配置，原因包括网络不稳定等，nixpkg中的包更新很难。使用p*o*y*h*i*s-ng结合v*r*y，在早上可以提高成功的概率。
  - [] 部署本地的nix 相关的cache和虚拟环境的管理。
- [] remote 支持, 可能需要基于vscode补充的能力，同时具有配置环境的问题，需要dind的能力。
  - [x] dev container 脚本运行。使用nvim asynctask 并配置justfile实现程序的运行。基于目录映射的脚本，实现结果的替换，并输入到quickfix中
  - [x] remote dap 实现程序的debug。debugpy 及相应的dap的配置目前已经支持。
  - [] remote lsp 支持，目前使用distant.nvim 方案，在dev-container环境出现bug，待作者反馈。
  - [] remote neotest 支持，目前python相关的config 比较复杂，待作者反馈。
  - [] ？或可以使用vscode实现remote的能力，同时用在ahk2 和vscode可以实现对应的跳转的能力，或者选者在vscode中执行，在nvim中进行修改。
  - [] 基于nix的环境隔离与基于docker的远程/环境隔离相配置，已有docker内容使用vscode处理，新内容基于nix构建环境
  - [] 基于nix的环境隔离与基于docker的远程/环境隔离相配置，已有docker内容使用vscode处理，新内容基于nix构建环境。
  - [] standalone 的neovim 的flake 化， nixvim 配置和vscode兼容使用的简版vim，可以方便的配置转换和大部分默认的跳转（flash和hop）
  - [] 详细梳理场景和操作流程，对vscode 和neovim+zellij 的快捷键的分配，减少心智负担

## 关于系统的结构
- host系统：Windows 11
基础环境要求：开启wsl，hyperv（optional），安装docker-desktop, ramddisk（注册），ramcache（注册），sourcecodepro字体，设置terminal使用该字体。绿色软件，twm（依赖conda和hk3)，终端，浏览器，编辑器，阅读器，git，代理，下载工具等常用必备高速工具集合。配置cpp库，方比那使用软件等https://zhuanlan.zhihu.com/p/618485834

 - docker 容器（wsl2）： nixpkg abled Ubuntu or nixos
 - 使用特定的volume 目录缓存所有的nixpkg, 并且需要以多用户的方式安装nix相关工具
 - 备份与恢复方案
Windows 11 使用WinNTSetup 写入到vhdx文件中，并对该文件进行备份，恢复是使用bootic 修改注册表引导到正确的磁盘文件。注册软件系统更新后会导致无法使用，需要在别的系统加载硬盘并重新使用reg/drv.bak/*.sys 覆盖systerm32/driver中的同名文件。更新完成后重新注册。
wsl中的系统，使用export和import进行备份和恢复，在host崩溃是，使用同版本系统进行export和import后，用已经存在的ext4.vhdx进行覆盖即可，目前只是使用复制和黏贴，使用重命名可能导致错误。

## 主要结果
 - [] 主要支持的文件类型，py，ipynb，md，tex，rst，json，org(neorg)，nix
 - [] 主要支持的语言，python，md，lua，dockfile，nix
 - [] 依据项目的不同，自动配置相应的终端和虚拟环境和shell与编辑器等，使用direnv(dev-env 目前有点过于复杂，待和devbox，fox 等测评后决定）或者vscode自带的功能。
 - [] 场景1：
 单文件的编辑（核心)。nvim配置主要的编辑功能和“视野”跳转。注释，代码段，git位置，lsp提示，lint和compile位置，ai辅助工具的使用。使用vscode-neovim插件，nvim接管normal等模式，vscode在插入模式下接管。
 单行（根据提示1-char 直接跳转到单词上）页内，包括不同的spits 中同样对待（2-char+指示字母跳转到指示位置， <jr>+指示字母，跳转到指定行， <jw>+指示字母跳转到指定单词）buffer内（/关键字搜素）
 “远程文本操作“： 基于flash 的命令
 基于hop的自定以命令

 - [] 场景2：
 代码浏览功能，主要依靠的是vscode的codetour插件，并使用相应的lsp的跳转功能。需要调整的快捷键进行统一。
 - [] 场景3：
 笔记和log功能
 - [] 场景4：
 文本写作：论文，blog等
 - [x] 技能点1: 跳转
    flash/leap和hop通用跳转，自动提示，t,f,%,*,等的增强插件
    文件之间的跳转，基于harpoon。
 - [] 技能点2: git 操作
    基于命令行（查看与简单操作），lazygit和nvim-fugitive 三种模式实现git的快捷操作。包括：stage，stash，pull，push，commit及编写规范，rebase，冲突消解，worktree支持，diff（文件，分支）
 - [] 技能点3: TDD 闭环
    在remote 模式下有限使用vscode，neovim实现有些困难
    lsp，lint，git，快速定位
    dap，test，终端上输出 error，使用并跳转
 - [] 技能点4: 高阶文本处理
     macro
     /以及vimgrep（或用其他更快的工具）
     自定义命令和text object
     综合使用
 - [] 技能点5: AI 辅助
     ChatGPT以及相应的代理配置，
     Copilot
     本地AI工具
     
pending:
1. 开发环境和发布环境的配置
从头开发的环境，使用基于nix的或者nix下的管理的一些环境配置的方法，实现只要配置一次环境就可以。并且可以自动的实现激活并在编辑器中进行使用。
使用docker container 或则flake/nix shell等方法发布环境（python可以结合使用使用poetry 这些工具）
2. 键盘使用习惯，尽量靠近vscode，并对其中的一些, 常用的快捷键可以进行键位的优化，进而提高效率。 
3. 详细梳理工作流，对全部的流程进行细节的分析，进而更准确地优化相应的环节。
4. 梳理重要的重复性的工作步骤，并对这些关键点进行优化
