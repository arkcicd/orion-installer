# orion-installer

## to use

* create cicd/installer directory in your repo 
* cd cicd/installer
* git submodule add <repo url>
* ln -s orion-installer/installer.yml installer.yml
* cp orion-installer/installer-config.yml to cicd/installer/installer-config.yml and edit
* cp orion-installer/added_tasks.yml.sample to cicd/installer/added_tasks.yml (if added tasks are needed)
* edit added_tasks.yml and add app-specific tasks for the installer

```
[root@ip-10-200-35-144 installer]# ls -la
total 8
drwxr-xr-x. 3 root root   78 Apr 19 13:51 .
drwxr-xr-x. 6 root root   67 Apr 19 13:13 ..
-rw-r--r--. 1 root root 4339 Apr 19 13:49 installer-config.yml
lrwxrwxrwx. 1 root root   29 Apr 19 13:51 installer.yml -> orion-installer/
installer.yml
drwxr-xr-x. 2 root root  136 Apr 19 13:51 orion-installer
[root@ip-10-200-35-144 installer]#
```

## license

This software is licensed under the MIT License.

see https://opensource.org/licenses/MIT

## invoke in Jenkinsfile

after checkout, b efore packer...

```

        stage('installer') {
            // execute ansible installer.yml play
            steps {
                script {
                    install_out = sh (
                        script: "cd cicd/installer/; ansible-playbook installer.yml",
                        returnStdout: true
                    )
                    echo "Install Output"
                    echo "${install_out}"
                }
            }
        }
```
