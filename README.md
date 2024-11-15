# Welcome to the SR Linux workshop at UW

This README is your starting point into the hands on section.

Pre-requisite: A laptop with SSH client and GitHub account (to use codespaces)

Shortcut links to major sections in this README:

|   |   |
|---|---|
| [Lab Topology](#lab-topology) | [Deploying the lab](#deploying-the-lab) |

## Lab Environment

---
<div align=center>
<a href="https://codespaces.new/sajusal/uw-workshop?quickstart=1">
<img src="https://gitlab.com/rdodin/pics/-/wikis/uploads/d78a6f9f6869b3ac3c286928dd52fa08/run_in_codespaces-v1.svg?sanitize=true" style="width:50%"/></a>

**[Run](https://codespaces.new/sajusal/uw-workshop?quickstart=1) this lab in GitHub Codespaces for free**.  
[Learn more](https://containerlab.dev/manual/codespaces/) about Containerlab for Codespaces.

</div>

---

## Workshop
The objective of the hands on section of this workshop is the following:
- Configure a leaf-spine fabric
- Configure VRFs
- Establish communication between the clients

## Lab Topology

![image](lab-topology.jpg)

## Deploying the lab

Click on the Codespaces icon above to create codespace VM for your lab.

After codespace VM is created, the repo will be automatically cloned to the VM and you will be taken directly into the repo directory.

Verify that the git repo files are available on your codespaces VM.

```bash
@sajusal ➜ /workspaces/uw-workshop (main) $ 
@sajusal ➜ /workspaces/uw-workshop (main) $ ls -lrt
total 108
-rw-rw-rw- 1 vscode root  1923 Nov 15 03:03 srl-uw.clab.yml
-rw-rw-rw- 1 vscode root 97320 Nov 15 03:03 lab-topology.jpg
-rw-rw-rw- 1 vscode root  4451 Nov 15 03:03 README.md
```

To deploy the lab, run the following:

```bash
cd uw-workshop/
sudo clab deploy -t srl-uw.clab.yml
```

[Containerlab](https://containerlab.dev/) will deploy the lab and display a table with the list of nodes and their IPs.

```bash
+---+---------+--------------+-------------------------------+---------------+---------+-----------------+-----------------------+
| # |  Name   | Container ID |             Image             |     Kind      |  State  |  IPv4 Address   |     IPv6 Address      |
+---+---------+--------------+-------------------------------+---------------+---------+-----------------+-----------------------+
| 1 | client1 | 7a23b8aacbf2 | ghcr.io/srl-labs/alpine       | linux         | running | 172.20.20.10/24 | 2001:172:20:20::10/64 |
| 2 | client2 | ff496107fb50 | ghcr.io/srl-labs/alpine       | linux         | running | 172.20.20.11/24 | 2001:172:20:20::11/64 |
| 3 | client3 | fc70070baca3 | ghcr.io/srl-labs/alpine       | linux         | running | 172.20.20.12/24 | 2001:172:20:20::12/64 |
| 4 | client4 | 4314b8703505 | ghcr.io/srl-labs/alpine       | linux         | running | 172.20.20.13/24 | 2001:172:20:20::13/64 |
| 5 | leaf1   | 18d2367c0bfe | ghcr.io/nokia/srlinux:24.10.1 | nokia_srlinux | running | 172.20.20.2/24  | 2001:172:20:20::2/64  |
| 6 | leaf2   | 5d69ffd0db22 | ghcr.io/nokia/srlinux:24.10.1 | nokia_srlinux | running | 172.20.20.3/24  | 2001:172:20:20::3/64  |
| 7 | spine1  | 0299e53187ba | ghcr.io/nokia/srlinux:24.10.1 | nokia_srlinux | running | 172.20.20.4/24  | 2001:172:20:20::4/64  |
| 8 | spine2  | b24abc3501b4 | ghcr.io/nokia/srlinux:24.10.1 | nokia_srlinux | running | 172.20.20.5/24  | 2001:172:20:20::5/64  |
+---+---------+--------------+-------------------------------+---------------+---------+-----------------+-----------------------+
```

To display all deployed labs on your VM at any time, use:

```bash
sudo clab inspect --all
```

## Connecting to the devices

Find the nodename or IP address of the device from the above output and then use SSH.

```bash
ssh leaf1
```

To login to the client, identify the client hostname using the `sudo clab inspect --all` command above and then:

```bash
sudo docker exec –it client3 sh
```

## SR Linux Configuration Mode

To enter candidate configuration edit mode in SR Linux, use:

```srl
enter candidate
```

To commit the configuration in SR Linux, use:

```srl
commit stay
```

Here's a reference table with some commonly used commands.

| Action | Command |
| --- | --- |
| Enter Candidate mode | `enter candidate {private}` |
| Commit configuration changes | `commit {now\|stay}` |
| | `now` – commits and exits from candidate mode |
| | `stay` – commits and stays in candidate mode |
| Delete configuration elements | `delete` |
| | Eg: `delete interface ethernet-1/5` |
| Discard configuration changes | `discard {now\|stay}` |
| Compare candidate to running | `diff running /` |
| View configuration in current mode & context | `info {flat}` |
| View configuration in another mode & context | `info {flat} from state /interface ethernet-1/1` |
| Output modifiers | `<command> \| as {table\|json\|yaml}` |
| Access Linux shell | `bash` |
| Find a command | `tree flat detail \| grep <keyword>` |

## Configure Interfaces

## Configure BGP

## Configure VRF
