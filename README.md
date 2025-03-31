# reproduction task docker-compose problems

## Setup

3 different folders with docker-compose files in them. Each file mounts the current folder into the container.

Environment:
* Ubuntu 24.04
* Docker and Task installed through https://docs.wakemeops.com/ 

Tested with:
* Docker version: 27.2.1 & 28.0.4
* Docker Compose: 2.29.2 & 2.34.0
* containerd.io: 1.7.21 & 1.7.26
* go-task: 3.41.0 & 3.42.1

## go-task 3.41.0

```bash
# make sure go-task 3.41.0 is installed
$ sudo apt install go-task=3.41.0-1~ops2deb
# go to folder and start all containers
$ cd this-folder
$ go-task all-start
```

The `ls -l` in each container should reflect all 3 different folders.

```text
task: [one-folder:start] docker-compose up --remove-orphans
[+] Running 3/3
 ✔ Network one-folder_default              Created                                                                       0.1s 
 ✔ Volume "one-folder_volume-one-folder"   Created                                                                       0.0s 
 ✔ Container one-folder-node-one-folder-1  Created                                                                       0.1s 
Attaching to node-one-folder-1
node-one-folder-1  | total 8
node-one-folder-1  | -rw-rw-r--    1 node     node           112 Mar 31 16:07 Taskfile.yml
node-one-folder-1  | -rw-rw-r--    1 node     node           257 Mar 31 16:05 docker-compose.yml
node-one-folder-1  | -rw-rw-r--    1 node     node             0 Mar 31 15:21 one-folder-file
node-one-folder-1 exited with code 0
task: [one-folder:start] docker-compose down -v
[+] Running 3/3
 ✔ Container one-folder-node-one-folder-1  Removed                                                                       0.0s 
 ✔ Volume one-folder_volume-one-folder     Removed                                                                       0.0s 
 ✔ Network one-folder_default              Removed                                                                       0.2s 
task: [another-folder:start] docker-compose up --remove-orphans
[+] Running 3/1
 ✔ Network another-folder_default                  Created                                                               0.1s 
 ✔ Volume "another-folder_volume-another-folder"   Created                                                               0.0s 
 ✔ Container another-folder-node-another-folder-1  Created                                                               0.0s 
Attaching to node-another-folder-1
node-another-folder-1  | total 8
node-another-folder-1  | -rw-rw-r--    1 node     node           112 Mar 31 16:07 Taskfile.yml
node-another-folder-1  | -rw-rw-r--    1 node     node             0 Mar 31 15:21 another-folder-file
node-another-folder-1  | -rw-rw-r--    1 node     node           269 Mar 31 16:05 docker-compose.yml
node-another-folder-1 exited with code 0
task: [another-folder:start] docker-compose down -v
[+] Running 3/3
 ✔ Container another-folder-node-another-folder-1  Removed                                                               0.0s 
 ✔ Volume another-folder_volume-another-folder     Removed                                                               0.0s 
 ✔ Network another-folder_default                  Removed                                                               0.2s 
task: [start] docker-compose up --remove-orphans
[+] Running 3/1
 ✔ Network this-folder_default               Created                                                                     0.1s 
 ✔ Volume "this-folder_volume-this-folder"   Created                                                                     0.0s 
 ✔ Container this-folder-node-this-folder-1  Created                                                                     0.0s 
Attaching to node-this-folder-1
node-this-folder-1  | total 8
node-this-folder-1  | -rw-rw-r--    1 node     node           477 Mar 31 16:07 Taskfile.yml
node-this-folder-1  | -rw-rw-r--    1 node     node           260 Mar 31 16:05 docker-compose.yml
node-this-folder-1  | -rw-rw-r--    1 node     node             0 Mar 31 15:20 this-folder-file
node-this-folder-1 exited with code 0
task: [start] docker-compose down -v
[+] Running 3/3
 ✔ Container this-folder-node-this-folder-1  Removed                                                                     0.0s 
 ✔ Volume this-folder_volume-this-folder     Removed                                                                     0.0s 
 ✔ Network this-folder_default               Removed                                                                     0.2s
```

## go-task 3.42.1

```bash
# make sure go-task 3.42.1 is installed
$ sudo apt install go-task=3.42.1-1~ops2deb
# go to folder and start all containers
$ cd this-folder
$ go-task all-start
```

The `ls -l` in each container should reflect all 3 different folders, but it shows in each case the folder of the initial taskfile.

```text
task: [one-folder:start] docker-compose up --remove-orphans
[+] Running 3/3
 ✔ Network one-folder_default              Created                                                                       0.1s 
 ✔ Volume "one-folder_volume-one-folder"   Created                                                                       0.0s 
 ✔ Container one-folder-node-one-folder-1  Created                                                                       0.0s 
Attaching to node-one-folder-1
node-one-folder-1  | total 8
node-one-folder-1  | -rw-rw-r--    1 node     node           477 Mar 31 16:07 Taskfile.yml
node-one-folder-1  | -rw-rw-r--    1 node     node           260 Mar 31 16:05 docker-compose.yml
node-one-folder-1  | -rw-rw-r--    1 node     node             0 Mar 31 15:20 this-folder-file
node-one-folder-1 exited with code 0
task: [one-folder:start] docker-compose down -v
[+] Running 3/3
 ✔ Container one-folder-node-one-folder-1  Removed                                                                       0.0s 
 ✔ Volume one-folder_volume-one-folder     Removed                                                                       0.0s 
 ✔ Network one-folder_default              Removed                                                                       0.2s 
task: [another-folder:start] docker-compose up --remove-orphans
[+] Running 3/3
 ✔ Network another-folder_default                  Created                                                               0.1s 
 ✔ Volume "another-folder_volume-another-folder"   Created                                                               0.0s 
 ✔ Container another-folder-node-another-folder-1  Created                                                               0.0s 
Attaching to node-another-folder-1
node-another-folder-1  | total 8
node-another-folder-1  | -rw-rw-r--    1 node     node           477 Mar 31 16:07 Taskfile.yml
node-another-folder-1  | -rw-rw-r--    1 node     node           260 Mar 31 16:05 docker-compose.yml
node-another-folder-1  | -rw-rw-r--    1 node     node             0 Mar 31 15:20 this-folder-file
node-another-folder-1 exited with code 0
task: [another-folder:start] docker-compose down -v
[+] Running 3/3
 ✔ Container another-folder-node-another-folder-1  Removed                                                               0.0s 
 ✔ Volume another-folder_volume-another-folder     Removed                                                               0.0s 
 ✔ Network another-folder_default                  Removed                                                               0.2s 
task: [start] docker-compose up --remove-orphans
[+] Running 3/0
 ✔ Network this-folder_default               Created                                                                     0.1s 
 ✔ Volume "this-folder_volume-this-folder"   Created                                                                     0.0s 
 ✔ Container this-folder-node-this-folder-1  Created                                                                     0.0s 
Attaching to node-this-folder-1
node-this-folder-1  | total 8
node-this-folder-1  | -rw-rw-r--    1 node     node           477 Mar 31 16:07 Taskfile.yml
node-this-folder-1  | -rw-rw-r--    1 node     node           260 Mar 31 16:05 docker-compose.yml
node-this-folder-1  | -rw-rw-r--    1 node     node             0 Mar 31 15:20 this-folder-file
node-this-folder-1 exited with code 0
task: [start] docker-compose down -v
[+] Running 3/3
 ✔ Container this-folder-node-this-folder-1  Removed                                                                     0.0s 
 ✔ Volume this-folder_volume-this-folder     Removed                                                                     0.0s 
 ✔ Network this-folder_default               Removed                                                                     0.2s 
```
