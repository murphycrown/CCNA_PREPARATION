CLI refers to the Command-line interface.It is the interface you use to configure Cisco devices.There is also an alternative called GUI for users who don't want to use commands for configuration.GUI stands for Graphical User Interface and it allows user to use buttons or input fields over commands.Even though, the  GUI is simpler than CLI , it is best practice to learn CLI for advanced configurations.

For setting up physical devices, network engineers usually use console ports to enter the CLI. They use **rollover cables** to connect to a Cisco device via RJ-45 console port.After plugging the cable in you need terminal emulator, in order to open the CLI. You can choose popular choices, such as [Putty](https://putty.org/index.html) .

## Inside the CLI
### User EXEC Mode

- `>` means you are in user exec mode.
By using user exec mode you can look at some things, but you won't be able to change anything.It is also called user mode.It doesn't specific for Cisco IOS, operating systems, such as Linux also use this mode.

Here is the list commands that is available in user exec mode.

![[user_exec_mode_commands.png]]

- `?` is used for viewing the available commands in current mode.
### Privileged EXEC mode

- `#` represents privileged exec mode.You can enter this mode by simply typing the command `enable` inside user exec mode.
Privileged exec mode provides complete access to view the device's configuration or restarting the device, but you still can't change the configuration.It allows you to do things, such as changing the time or saving the configuration file or etc.

Here is the list commands that is available in privileged exec mode.

![[privileged_exec_mode_commands.png]]

### Global Configuration Mode

- `(config) #` shows that you are in the Global Configuration Mode.You can enter this mode by simple typing `configure terminal` inside privileged mode.
Global Configuration mode gives you an ability to change network configurations as well as doing things, such as settings passwords.Let's look at some of the commands we can use inside this mode.
* By putting `do` in front of the privileged exec mode commands you can use them in global configuration mode.

- `enable password` allows you to set the password for privileged exec mode, so no one else except you can access it.It consider as best practice, in terms of security.

- There are types of configuration file kept on the device: Running-config and Startup-config.
	1. **Running-config** refers to the current configuration file.When you enter the commands inside the CLI, you are actually editing this file.You can see this file by simply typing `show running-config` inside the Privileged Exec Mode.

	2. **Startup-config** is a configuration file that will be loaded upon restart of the device.`show startup-config` command is used for displaying this file.

- There are three ways for saving the running configuration: `write`, `write memory` and `copy running-config startup-config`. All of these commands perform same action despite of their differences.However, it is possible that you see some of those commands in different operating systems, because each of them is being used by different manufacturers.

- As we know, the output shows our password when we display the running-config or startup-config file.For security reason we don't want it to be shown as a text, so we enter the global configuration mode and use `service password-encryption` command to ensure our password is stored encrypted.Here is what happens when we type `show running-config` after enabling password encryption.

![[show_running-config_output.png]]
- **7** shows that it uses Cisco's proprietary encryption algorithm. 

- Even though `service password-encryption` command stores passwords encrypted, it is not the best practice ,because these ciphers can be reversed within seconds.However, we can use secrets to increase the level of security.Simply setting the passwords by using `enable secret` command we can make sure that out password is stored more securely.Here is the running-config file when we implement these features.

![[show_running_config_output_secret.png]]
- **5** means that it uses MD5 encryption algorithm. MD5 algorithm itself is not entirely secure according to NIST (National Institute of Standards and Technologies) due to the number of collisions, but it's much more secure than using cisco's default encryption algorithm.

- Notice that both `enable secret` and `enable password` commands are display, but if we configured both of them , `enable password`  will be ignored.In addition, `service password-encryption` command has no effect on secrets.Secrets are always encrypted by default.

- If you want to disable or remove the command you previously configured in the CLI you can do this by putting `no` in front of the command.However, this doesn't undo the previous services that has been done by this command.It only applies for future services.

See all the commands and their function in [[Cisco Switch CLI commands]].