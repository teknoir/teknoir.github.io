---
title: Device logs
layout: single
toc: true
categories:
  - troubleshooting
tags:
  - troubleshooting-devices
  - troubleshooting
---

## Device logs
Accessing system or app logs can make the situation clearer. Here is a guide on how to do that!

### System logs
Listing boots, run:

```bash
journalctl --list-boots
```

If boot logs are not persisted, you will only see the latest(current) log here.

#### Persisting logs between boots

To set journald to persist logs update config:

```bash
nano /etc/systemd/journald.conf
```

Change:

```bash
#Storage=auto
```

To:

```bash
Storage=auto
```

After a reboot, list again:

```bash
journalctl --list-boots
-1 79622793901341d1a6e98ce3258398e9 Sun 2022-02-20 09:44:01 UTC—Fri 2022-03-11 20:29:58 UTC
0 ea8b6696821c4fc0a51bc832915e1095 Fri 2022-03-11 20:29:58 UTC—Fri 2022-03-11 20:35:04 UTC
```

To list logs for -1 (Sun 2022-02-20 09:44:01 UTC—Fri 2022-03-11 20:29:58 UTC) you run:

```bash
journalctl -b 1
```

#### Listing logs for a specific service

Example of services that can be of interest:
 * ModemManager
 * NetworkManager
 * tns
 * k3s
 
##### TNS

To list current logs for TekNoir Subsystems check service:

```bash
journalctl -b 0 -u tns
```

or for legacy systems, run:

```bash
journalctl -b 0 -u tns@wwan0
```

###### K3s

To follow logs for K3s(Kubernetes):

```bash
journalctl -b 0 -f -u k3s
```

###### ModemManager

To follow logs for ModemManager:

```bash
journalctl -b 0 -f -u ModemManager
```

And similar for NetworkManager

### App logs, in kubernetes

Teknoir subsystems all run in K3s, a version of Kubernetes by Rancher.

**Note:** that you have to be root for the following commands!!! Please check out the 
[access](/troubleshooting/#device-access) section for how to elevate permissions.
{: .notice--info}

#### Status

To check system pods run:

```bash
kubectl -n kube-system get pods
```

If all is ok it should look something like:

```bash
NAME                                          READY     STATUS      RESTARTS      AGE
calico-node-gv7c4                             1/1       Running     0             83m
coredns-96cc4f57d-t6lfb                       1/1       Running     0             83m
local-path-provisioner-84bb864455-7d966       1/1       Running     0             83m
mqtt-c8b5788b8-bcrq2                          1/1       Running     0             83m
toe-75d96cdb84-v7r26                          1/1       Running     1 (80m ago)   83m
calico-kube-controllers-66c96654f5-vlksc      1/1       Running     0             83m
metrics-server-ff9dbcb6c-2dpzb                1/1       Running     0             83m
healtcheck                                    1/1       Running     0             80m
```

If the device is starting up and you want to monitor status of pods you can run:

```bash
watch kubectl -n kube-system get pods
```

If you need to monitor user created pods, created from the device config, from the Devstudio in our platform.

```bash
kubectl get pods
```

This is something you could then see, but also, there could be pods missing for example.

```bash
NAME                                         READY     STATUS      RESTARTS     AGE
hardware-c68c9b556-lwdc9                     1/1       Running     0            85m
reverse-tunnel-546877479f-cs9sj              1/1       Running     0            85m
```

Pods have different statuses and as long as it does not say Error of some kind it is probably fine.

##### Describe pod

If a pod has an error describing the pod might help, like this:

```bash
kubectl -n kube-system describe pod toe-84c56d659b-gzrsc
```

The pods name is taken from the status listing above.

A healthy pod looks like this:

```bash
Name:         toe-84c56d659b-gzrsc
Namespace:    kube-system
Priority:     0
Node:         vmv3-a1001/10.33.136.48
Start Time:   Mon, 18 Apr 2022 13:15:12 +0000
Labels:       app=toe
              pod-template-hash=84c56d659b
Annotations:  cni.projectcalico.org/containerID: e6ef539a0d8a8144c2bcaa5bf3fc2976982ace4c3a7fcf75ad5d744a6a09530d
              cni.projectcalico.org/podIP: 10.42.104.144/32
              cni.projectcalico.org/podIPs: 10.42.104.144/32
Status:       Running
IP:           10.42.104.144
IPs:
  IP:           10.42.104.144
Controlled By:  ReplicaSet/toe-84c56d659b
Containers:
  toe:
    Container ID:   containerd://92b9a78319ca03e2a911c95ee358feb21f051636f9d6ea0cfb55444f5bb4183d
    Image:          gcr.io/teknoir/toe:latest
    Image ID:       gcr.io/teknoir/toe@sha256:5940d4a49a67271e8db1fffe78fde8066995dd5e18fe26f9625c69b0b41f15ec
    Port:           <none>
    Host Port:      <none>
    State:          Running
      Started:      Wed, 01 Jun 2022 05:38:25 +0000
    Last State:     Terminated
      Reason:       Error
      Exit Code:    1
      Started:      Tue, 31 May 2022 17:38:18 +0000
      Finished:     Wed, 01 Jun 2022 05:38:22 +0000
    Ready:          True
    Restart Count:  42
    Environment:
      TOE_PROJECT:       teknoir
      TOE_IOT_REGISTRY:  avangard-production
      TOE_DEVICE:        vmv3-a1001
      TOE_CA_CERT:       /etc/teknoir/roots.pem
      TOE_PRIVATE_KEY:   /etc/teknoir/rsa_private.pem
    Mounts:
      /etc/teknoir from toe-volume (rw)
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-mtglz (ro)
Conditions:
  Type              Status
  Initialized       True
  Ready             True
  ContainersReady   True
  PodScheduled      True
Volumes:
  toe-volume:
    Type:          HostPath (bare host directory volume)
    Path:          /etc/teknoir
    HostPathType:
  kube-api-access-mtglz:
    Type:                    Projected (a volume that contains injected data from multiple sources)
    TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    ConfigMapOptional:       <nil>
    DownwardAPI:             true
QoS Class:                   BestEffort
Node-Selectors:              <none>
Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
                             node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:                      <none>
```

The list of events at the bottom would display any errors.

##### App(POD) logs

If you need to look at logs for a pod

```bash
kubectl logs reverse-tunnel-546877479f-cs9sj
```

The pods name is taken from the status listing above.

To tail a pods logs, continuously following the log just add the flag for it:

```bash
kubectl logs -f reverse-tunnel-546877479f-cs9sj 
```