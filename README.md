
<h1 class="entry-title">How To Install Grafana on Ubuntu 22.04|20.04|18.04</h1>

<h3 id="mce_10">Step 1: Update system</h3>
<p>Ensure your Ubuntu system is up to date.</p>

```
sudo apt update
```

<h3>Step 2: Add Grafana APT repository</h3>
<p>Add Grafana gpg key which allows you to install signed packages.</p>

```
sudo apt install -y gnupg2 curl software-properties-common
curl -fsSL https://packages.grafana.com/gpg.key|sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/grafana.gpg
```

<p>Then install Grafana APT repository:</p>

```
sudo add-apt-repository "deb https://packages.grafana.com/oss/deb stable main"
```

<h3>Step 3: Install Grafana on Ubuntu 22.04|20.04|18.04</h3><br />

<p>Once the repository is added, proceed to update your Apt repositories and install Grafana</p>

```
sudo apt update
sudo apt -y install grafana
```

<p>Start Grafana service.</p>

```
sudo systemctl enable --now grafana-server
```

<p>The service should now be running.</p>

```
systemctl status grafana-server.service
```

```
● grafana-server.service - Grafana instance
     Loaded: loaded (/lib/systemd/system/grafana-server.service; enabled; vendor preset: enabled)
     Active: active (running) since Fri 2022-10-14 16:26:13 EAT; 4s ago
       Docs: http://docs.grafana.org
   Main PID: 5541 (grafana-server)
      Tasks: 7 (limit: 9460)
     Memory: 41.7M
        CPU: 784ms
     CGroup: /system.slice/grafana-server.service
             └─5541 /usr/sbin/grafana-server --config=/etc/grafana/grafana.ini --pidfile=/run/grafana/grafana-server.pid --packaging=deb cfg:default.paths.logs=/var/log/grafana cfg:default.paths.da&gt;

Oct 14 16:26:15 jammy grafana-server[5541]: logger=live.push_http t=2022-10-14T16:26:15.390848521+03:00 level=info msg="Live Push Gateway initialization"
Oct 14 16:26:15 jammy grafana-server[5541]: logger=infra.usagestats.collector t=2022-10-14T16:26:15.666309404+03:00 level=info msg="registering usage stat providers" usageStatsProvidersLen=2
Oct 14 16:26:15 jammy grafana-server[5541]: logger=server t=2022-10-14T16:26:15.669532612+03:00 level=info msg="Writing PID file" path=/run/grafana/grafana-server.pid pid=5541
Oct 14 16:26:15 jammy grafana-server[5541]: logger=provisioning.alerting t=2022-10-14T16:26:15.670221114+03:00 level=info msg="starting to provision alerting"
Oct 14 16:26:15 jammy grafana-server[5541]: logger=provisioning.alerting t=2022-10-14T16:26:15.670379505+03:00 level=info msg="finished to provision alerting"
Oct 14 16:26:15 jammy grafana-server[5541]: logger=http.server t=2022-10-14T16:26:15.683158306+03:00 level=info msg="HTTP Server Listen" address=[::]:3000 protocol=http subUrl= socket=
Oct 14 16:26:15 jammy grafana-server[5541]: logger=ngalert t=2022-10-14T16:26:15.683496864+03:00 level=info msg="warming cache for startup"
Oct 14 16:26:15 jammy grafana-server[5541]: logger=ticker t=2022-10-14T16:26:15.683796068+03:00 level=info msg=starting first_tick=2022-10-14T16:26:20+03:00
Oct 14 16:26:15 jammy grafana-server[5541]: logger=grafanaStorageLogger t=2022-10-14T16:26:15.692317758+03:00 level=info msg="storage starting"
Oct 14 16:26:15 jammy grafana-server[5541]: logger=ngalert.multiorg.alertmanager t=2022-10-14T16:26:15.692975064+03:00 level=info msg="starting MultiOrg Alertmanager"
```


<h3>Step 4: Open Port on Firewall (Optional)</h3>
<p>Grafana default http port is <strong>3000,</strong>&nbsp;you’ll need to allow access to this port on the firewall. Ubuntu comes with ufw firewall. For Debian, you can install it using: </p>


```
sudo apt -y install ufw
```


<p>Then enable the firewall service:</p>

```
sudo ufw enable
```

```
sudo ufw allow ssh
sudo ufw allow 3000/tcp
```

<p>To allow access only from a specific subnet, use:</p>

```
sudo ufw allow from 192.168.50.0/24 to any port 3000
```

<h3>Step 5: Access Grafana Dashboard on Ubuntu<meta charset="utf-8">2<meta charset="utf-8">2.04|20.04|18.04</h3>
<p>Default logins are:</p>

![Screenshot 2023-01-23 at 19 25 57](https://user-images.githubusercontent.com/22194506/214039200-7e64c47e-6009-49a9-896a-1dfcb7b5ee74.png)


```
Username: <mark style="background-color:initial" class="has-inline-color has-vivid-cyan-blue-color">admin</mark>
Password: <mark style="background-color:initial" class="has-inline-color has-vivid-purple-color">admin</mark>
```


<h4>Grafana Package details:</h4>
<ul>
    <li>Installs binary to&nbsp;<code>/usr/sbin/grafana-server</code></li>
    <li>Installs Init.d script to&nbsp;<code>/etc/init.d/grafana-server</code></li>
    <li>Creates default file (environment vars) to&nbsp;<code>/etc/default/grafana-server</code></li>
    <li>Installs configuration file to&nbsp;<code>/etc/grafana/grafana.ini</code></li>
    <li>Installs systemd service (if systemd is available) name&nbsp;<code>grafana-server.service</code></li>
    <li>The default configuration sets the log file at&nbsp;<code>/var/log/grafana/grafana.log</code></li>
    <li>The default configuration specifies a sqlite3 db at&nbsp;<code>/var/lib/grafana/grafana.db</code></li>
    <li>Installs HTML/JS/CSS and other Grafana files at&nbsp;<code>/usr/share/grafana</code></li>
</ul>

<p>The systemd service file and init.d script both use environment vars on the file located at <strong>/etc/default/grafana-server.</strong></p>
