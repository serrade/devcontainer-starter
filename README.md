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

## Setup (Podman + Dev Containers)

You don't need Docker Desktop. [Podman](https://podman.io/) is a free, open-source container engine that works seamlessly with VS Code Dev Containers on Windows, macOS, and Linux. Expand the dropdown for your operating system in each step.

### 1. Install Git

Git is what you'll use to download the project and switch between starter branches.

<details>
<summary><strong>Windows</strong></summary>

Download and run the installer:

https://git-scm.com/download/win

The defaults during install are fine.

</details>

<details>
<summary><strong>macOS</strong></summary>

The easiest path is the Xcode Command Line Tools, which include Git. In Terminal:

```bash
xcode-select --install
```

Or, if you already use [Homebrew](https://brew.sh/):

```bash
brew install git
```

</details>

<details>
<summary><strong>Linux</strong></summary>

Install Git via your distribution's package manager:

- Debian / Ubuntu: `sudo apt install git`
- Fedora: `sudo dnf install git`
- Arch: `sudo pacman -S git`

See https://git-scm.com/download/linux for other distros.

</details>

Open a new terminal and confirm it works:

```bash
git --version
```

### 2. Install Podman Desktop

Podman is the container engine; Podman Desktop is the cross-platform GUI that bundles it.

<details>
<summary><strong>Windows</strong></summary>

Download and run the installer:

https://podman-desktop.io/downloads

> Requirements: Windows 10 build 19043+ or Windows 11, plus admin rights to enable WSL 2 or Hyper-V the first time.

</details>

<details>
<summary><strong>macOS</strong></summary>

Download the Universal `.dmg` (works on Intel and Apple Silicon) and drag Podman Desktop into Applications:

https://podman-desktop.io/downloads/macos

> If you previously installed Podman via Homebrew, uninstall it first to avoid conflicts &mdash; the `.dmg` is the recommended install path.

</details>

<details>
<summary><strong>Linux</strong></summary>

Flatpak is the recommended install path:

```bash
flatpak remote-add --if-not-exists --user flathub https://flathub.org/repo/flathub.flatpakrepo
flatpak install --user flathub io.podman_desktop.PodmanDesktop
```

Launch it with `flatpak run io.podman_desktop.PodmanDesktop`. AppImage and tar bundles are also available at https://podman-desktop.io/downloads/linux.

If you prefer the CLI only, you can skip Podman Desktop entirely and install plain `podman` via your package manager (`sudo apt install podman`, `sudo dnf install podman`, ...). The Dev Containers extension only needs the `podman` binary on `PATH`.

</details>

Open Podman Desktop after install. It will walk you through creating a "Podman machine" (a small Linux VM that runs your containers under the hood &mdash; required on Windows and macOS, not needed on Linux where containers run natively). The defaults are fine.

### 3. Install VS Code

If you don't already have it, download for your platform here:

https://code.visualstudio.com/

### 4. Install the Dev Containers extension

Inside VS Code, install **Dev Containers** by Microsoft:

https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers

(Or open the Extensions panel with `Ctrl+Shift+X` / `Cmd+Shift+X` on macOS and search for "Dev Containers".)

### 5. Point Dev Containers at Podman

Open VS Code Settings with `Ctrl+,` (Windows / Linux) or `Cmd+,` (macOS), click the **Open Settings (JSON)** icon in the top-right of that tab, and add these two lines inside the outer `{}`:

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

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for how to add a new starter and how to keep variant branches in sync with `main`.
