# 139. Setting up MySQL
Created Tuesday 21 March 2023 at 11:04 pm

MySQL
1. Install MySQL server, the community editions. Remember to save the password somewhere. [Steps](https://www.digitalocean.com/community/tutorials/how-to-install-mysql-on-ubuntu-20-04)
2. Install MySQL workbench. Snap is available for Ubuntu - `sudo snap install mysql-workbench-community`. The Snap is sandboxed by default, and so, provide permissions by running `sudo snap connect mysql-workbench-community:password-manager-service :password-manager-service`. [Source](https://askubuntu.com/a/1242777/976489)

- To run MySQL in REPL mode: run `mysql -u root -p` and enter the password (stored earlier)
- To run MySQL Workbench, either run `mysql-workbench-community` in the terminal or open it from "Applications"(GUI). The default database is already present as an entry.