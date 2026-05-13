# devcontainer-starter

A multi-language [VS Code Dev Container](https://code.visualstudio.com/docs/remote/dev-containers) starter. Pick the branch that matches the stack you want to work in, open the folder in VS Code, and you're dropped straight into a ready-to-go container with the right tools and editor settings.

## Pick your starter

Each branch is a complete, self-contained starter. Check out the branch you want **before** opening the folder in VS Code.

| Branch | What's inside |
| --- | --- |
| [`main`](https://github.com/serrade/devcontainer-starter/tree/main) | Generic Ubuntu base container with a custom bash prompt, common CLI tools (`git`, `curl`, `jq`, `htop`, ...) and Fira Code. Use as the starting point for any new variant. |
| [`python`](https://github.com/serrade/devcontainer-starter/tree/python) | Everything in `main`, plus Python 3, pip, FastAPI / SQLAlchemy, and a PostgreSQL + Redis stack wired up via docker-compose. |
| [`terraform`](https://github.com/serrade/devcontainer-starter/tree/terraform) | Stub branch &mdash; Terraform tooling coming soon. |

```bash
git clone https://github.com/serrade/devcontainer-starter.git
cd devcontainer-starter
git switch python    # or main, terraform, ...
```

## Setup on Windows (Podman)

You don't need Docker Desktop. [Podman](https://podman.io/) is a free, open-source container engine that works seamlessly with VS Code Dev Containers.

### 1. Install Git

Git is what you'll use to download the project and switch between starter branches. Download the Windows installer and run it:

https://git-scm.com/download/win

The defaults during install are fine. Once it's done, open a new PowerShell window and confirm it works:

```powershell
git --version
```

### 2. Install Podman Desktop

Download the Windows installer and run it:

https://podman-desktop.io/downloads

Open Podman Desktop after install. It will walk you through creating a "Podman machine" (a small Linux VM that runs your containers under the hood). The defaults are fine &mdash; just click through.

> Requirements: Windows 10 build 19043+ or Windows 11, plus admin rights to enable WSL 2 or Hyper-V the first time.

### 3. Install VS Code

If you don't already have it:

https://code.visualstudio.com/

### 4. Install the Dev Containers extension

Inside VS Code, install **Dev Containers** by Microsoft:

https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers

(Or open the Extensions panel with `Ctrl+Shift+X` and search for "Dev Containers".)

### 5. Point Dev Containers at Podman

In VS Code, press `Ctrl+,` to open Settings, click the **Open Settings (JSON)** icon in the top-right of that tab, and add these two lines inside the outer `{}`:

```json
"dev.containers.dockerPath": "podman",
"dev.containers.dockerComposePath": "podman-compose"
```

Save the file. VS Code will now use Podman everywhere it would have used Docker.

### 6. Open the project in a container

1. **File &rarr; Open Folder...** and pick the cloned `devcontainer-starter` folder.
2. VS Code should show a notification: **"Folder contains a Dev Container configuration file. Reopen folder to develop in a container."** Click **Reopen in Container**.
   - If you miss the popup, click the green `><` icon in the bottom-left of the VS Code window and choose **Reopen in Container**.
3. The first build downloads the base image and installs packages &mdash; expect a few minutes. After that, the integrated terminal drops you inside the container with everything ready.

## Optional VS Code extensions for Podman

Neither of these is required to use this starter, but they're nice if you want a GUI for managing containers from inside VS Code:

- [**Container Tools**](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-containers) (Microsoft) &mdash; evolved from the Docker extension, supports Podman, Containerfile / Dockerfile syntax highlighting, image building.
- [**Pod Manager**](https://marketplace.visualstudio.com/items?itemName=dreamcatcher45.podmanager) (community) &mdash; GUI for managing Podman containers, images, volumes, networks, and compose stacks.

## Contributing a new starter

1. Branch off `main`: `git switch main && git switch -c <language>`.
2. Add the language-specific bits to `.devcontainer/` and any sample files at the repo root.
3. Push the branch: `git push -u origin <language>`.
4. Update the branch table in this README (on `main`) so the new starter is discoverable.

Generic improvements (new shell alias, new base tool, doc updates) go on `main` first and then propagate forward into each variant branch.
