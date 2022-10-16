### Using Docker desktop
To delete a container in docker desktop, you have to navigate to `containers` in the navigator, and you will be presented with a list of containers in a table. The last column of each row has some action buttons, one of which is a trash can button.

If you press that trash can button, it will prompt you to delete that specific container.

### Using the CLI
You can also delete a container using the docker CLI in a console window. You can do this using the command: `docker rm <container_name>`. The `<container_name>` part must be replaced by the name of the container that you want to delete, which can be found in the container listing [[Listing all containers]]