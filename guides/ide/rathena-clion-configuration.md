# rAthena CLion Configuration

If you are using CLion, we can configure the rAthena project for this IDE.

This guide will help you to:

- Configure CLion IDE to support rAthena
- Setup the server configurations
- Start the server in debug mode

### CLion project setup

After we cloned [rAthena repository](https://github.com/rathena/rathena), we can open it in CLion IDE.
CLion sees Makefile in the project root directory and will automatically try to configure the project,
but we need to do some additional steps to make it work.

#### Configure Makefile in the CLion settings

1. Open your Makefile settings (**File → Settings → Build, Execution, Deployment → Makefile**),
2. Set the **Toolchain** as a default toolchain for the project,
3. Set the **Build directory** to the root of the project,
4. Set the **Build options** to `--makefile=Makefile`,
5. In the section **Commands** input of the _Pre-configuration commands executed to generate the Makefile_
   section, add this:
    ```
    #!/bin/sh
    #
    # GNU Autotools template, feel free to customize.
    #
    which autoreconf >/dev/null && autoreconf --install --force --verbose "${PROJECT_DIR:-..}" 2>&1; /bin/sh "${PROJECT_DIR:-..}/configure" 
    ```
6. Set the **Build target** to `server`,
7. Set the **Clean target** to `clean`.
8. Click `Apply` and `OK`.

Thus, everything should look like this:

![CLion makefile settings](https://i.postimg.cc/h4zCDLx1/CLion-makefile-settings.png)

After we did that, CLion should be able to index project files and build it successfully.

!!! tip "You can also add any program arguments if you need it."


To run the server in CLion, I recommend relying on the next step in this guide.

### Server setup

After we configured CLion to build and index our project files, we can setup the server startup.
And to make the server startup work, we need to add a small adjustment to the configurations CLion has detected.
As CLion detected many run options – the most convenient one is to run login, map and char
servers separately to make the debugging later on easier.
So to run login, map, and char servers separately, we need to adjust the configuration to the relevant server configuration.

As an example, let's say we want to run the login server.
To do that, follow these steps:

1. At the top of the screen, click **Run → Edit Configurations**,
2. In the configuration list, select the **Login** configuration,
3. In the **Target** dropdown, check that the `login` target is selected,
4. In the **Executable**, click on the `...` button and then select the `login-server`
   file which is located in the root of the project,
5. Click `Apply` and `OK`.

!!! note

    Repeat the same steps for the map and char servers with the **Target** and **Executable** to the relevant server.

That's it! Now you can start the servers directly from CLion by selecting each configuration and clicking the green arrow.
Or you can run the server by pressing `Shift + F10`.

!!! tip "You can also add some extra options in the **Before launch** section to if you need it."

### Debugging the server

In the CLion IDE we can also debug the server.

If you don't know what debugging is – check out [this section](https://rathena.github.io/user-guides/debugging/#what-is-debugging).

As we created a separate configuration for each server, we can debug them separately, which makes debugging much easier.

To debug the server, you can run the server in the debug mode, which is the green bug icon in the top right corner after the play button.
Or you can just press `Shift + F9` to start the debugging.

In the CLion debugger mode you can evaluate expressions, use non-suspended breakpoints, etc.

!!! tip "You can find more information about debugging in the [CLion documentation](https://www.jetbrains.com/help/clion/debugging-code.html#useful-debugger-shortcuts)."