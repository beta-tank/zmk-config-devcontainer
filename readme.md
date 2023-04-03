

# ZMK config with GH Actions, Devcontainer and Codespaces integrations

[![Open in GitHub Codespaces](https://github.com/codespaces/badge.svg)](https://github.com/codespaces/new?hide_repo_select=true&ref=main&repo=623034386)

I'm tired of [ZMK toolchain setup](https://zmk.dev/docs/development/setup) in Docker on a new machine (cofiguring west, creating a Docker volume for my zmk-cofig repo folder, updating scripts for my shields and etc).

So I created this example repo that supports the following features:

- Building firmare using Github Actions (like many other repos do)
- [NEW] Run a fully configured ZMK build environment in a local [devcontainer](https://containers.dev/) with your zmk-config
- [NEW] Run a fully configured ZMK build environment in [Github Codespaces](https://github.com/features/codespaces) with your zmk-config
- [NEW] Scripts for building firmware for your shields with one terminal command

# How to start

1. Fork this repo
2. Add your shields' configurations to `/config/shields` folder (if you don't use preconfigured ZMK shields)

# Usage

## Using with Github Actions

1. Add all board+shield pairs that you want to build in a CI
2. If you want, tune `.github/workflows/build.yml` workflow
3. Push updates of your configs to the repo
4. Go to `Actions` section of your repo
5. Open `Build` workflow
6. Download `firmawe.zip` archive from `Artifacts` section

Out of the box Action is triggered by new commits in `main` branch and opened/reopened PRs.

## Using with local devcontainer

*Tested on Windows 10 with WSL2 and VS Code.*

This devcontainer is preconfigured to clone and setup ZMK installation within the container and update sources during the launching process. You can edit configuration in `.devcontainer/devcontainer.json`

1. Clone you repo locally
2. Open repo folder in VS Code (JetBrains IDEs not tested)
3. Open Command Palette (Ctrl+Shift+P) and run `Dev Containers: Open Folder in Container...` or click on a prompt in the bottom-right corner of the VS Code window
4. Wait until the building process is complete
5. Open a new terminal and run the build script (see the next sections)

## Codespace

You can develop ZMK FW in a web-browser or in VS Code without local environment setup.

1. Create Codespace according to [this instruction](https://docs.github.com/en/codespaces/developing-in-codespaces/creating-a-codespace-for-a-repository) (I have already put a devcontainer configuration into the repo)
2. Open Codespace in a web-browser or in VS Code (Command Palette (Ctrl+Shift+P) `Connect to Codespace...`)
3. Wait until the building process is complete
4. Open a new terminal and run the build script (see the next sections)

# Build scripts 

Scripts are located in `.devcontainer/.bashrc` and are automatically loaded on the container build stage.

Define your function like this:

```
build-test(){
    base-build nrfmicro_13 test-board
}
```

Where:

- build-test - name of a function
- nrfmicro_13 - board name
- test-board - shield name

Then you can start building by running the function by its name (`build-test` for example) in a terminal inside the container.

Compiled UF2 files are located in `build` folder.

Also you can start building by passing board and shield names as parameters to `base-build` function

```
base-build nrfmicro_13 test-board
```

If you update `.bashrc` then you should run `Rebuild container` in Command Palette (Ctrl+Shift+P)