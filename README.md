# VSCODESPACE

---

The Goal is to create with vscode devcontainer an universal workspace for datascience.

---
## Deployement
1. terminal cli : `git clone https://github.com/qwarksky/vscodespace.git`
2. In vscodespace directory run : `code .`
3. vscode => `[Ctrl]+[Shift]+P` : panel to run commande
4. vscode => Search : `Dev Containers: Rebuild and Reopen in Container`

## Documentation

* devcontainers : 
	* https://code.visualstudio.com/docs/devcontainers/containers
* UV : 
	* https://docs.astral.sh/uv/guides/integration/docker/
	* https://docs.astral.sh/uv/guides/integration/docker/#available-images
* Marimo notebook : 
	* https://docs.marimo.io/guides/deploying/prebuilt_containers/
	* https://docs.marimo.io/guides/deploying/deploying_docker/#prerequisites

## CLI :
* listing vscode extensions : `code --list-extensions`
* listing installed extensions : `code --list-extensions | % { "$_" }`
