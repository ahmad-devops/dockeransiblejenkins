#issue 1

TASK [Gathering Facts] *********************************************************
fatal: [server1]: UNREACHABLE! => {"changed": false, "msg": "Failed to connect to the host via ssh: jenkins@127.0.0.1: Permission denied (publickey,password).", "unreachable": true}

Fix -- 

1. update inventory file -- dev.ini with ansible_user=jenkins
#https://www.australtech.net/ansible-failed-to-connect-to-the-host-via-ssh/
2. since I was running on same host jenkins .ssh/id_ras.pub key should be added to jenkins.ssh/authorized_keys

#issue 2

TASK [Gathering Facts] *********************************************************
fatal: [127.0.0.1]: FAILED! => {"msg": "Missing sudo password"}

add below in visudo as we are running locally
jenkins     ALL=(ALL) NOPASSWD:ALL

#issue3

fatal: [127.0.0.1]: FAILED! => {"changed": false, "msg": "An unexpected requests error occurred when docker-py tried to talk to the docker daemon: 500 Server Error: Internal Server Error (\"b'{\"message\":\"Cannot locate specified Dockerfile: Dockerfile\"}'\")"}

Fix - The issue is jenkins is not able to read the . path . 
hence I have updated the playbook to use WORKSPACE directory as the path for Dockerfile.

Check jenkinsfile for more.
