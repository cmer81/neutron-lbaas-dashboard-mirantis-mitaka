Add LBaaS panels to Dashboard Mitaka Mirantis!
===================


The Dashboard panels for managing ***LBaaS v2*** are available starting with the Mitaka **Mirantis** release, after install plugins [LBaaS plugin for fuel](https://github.com/openstack/fuel-plugin-neutron-lbaas)

----------



*LBaaS v2 has several new concepts to understand:*

![alt text](http://docs.openstack.org/mitaka/networking-guide/_images/lbaasv2-diagram.png "Lbaasv2")

**Load balancer**
- *The load balancer occupies a neutron network port and has an IP address assigned from a subnet.*

**Listener**
- *Load balancers can listen for requests on multiple ports. Each one of those ports is specified by a listener.*

**Pool**
- *A pool holds a list of members that serve content through the load balancer.*

**Member**
- *Members are servers that serve traffic behind a load balancer. Each member is specified by the IP address and port that it uses to serve traffic.*

**Health monitor**
- *Members may go offline from time to time and health monitors divert traffic away from members that are not responding properly. Health monitors are associated with pools.*

LBaaS v2 has multiple implementations via different service plug-ins. The two most common implementations use either an agent or the Octavia services. Both implementations use the LBaaS v2 API.

----------

**On your Controller**
-------------

Clone the neutron-lbaas-dashboard repository and check out the release branch that matches the installed version of Dashboard:
```
apt-get install -y git
cd /usr/local/src/sahara-dashboard
git clone https://git.openstack.org/openstack/neutron-lbaas-dashboard
cd neutron-lbaas-dashboard
git checkout origin/stable/mitaka
```
Install the Dashboard panel plug-in:
```
python setup.py install
```
Copy the `_1481_project_ng_loadbalancersv2_panel.py` file from the `neutron-lbaas-dashboard/enabled` directory into the Dashboard `openstack_dashboard/local/enabled` directory.

```
cp neutron_lbaas_dashboard/enabled/_1481_project_ng_loadbalancersv2_panel.py /usr/share/openstack-dashboard/openstack_dashboard/local/enabled/
```

Enable the plug-in in Dashboard by editing the **local_settings.py** file and setting **enable_lb** to **True** in the **OPENSTACK_NEUTRON_NETWORK** dictionary.
```
vim /etc/openstack-dashboard/local_settings.py
```
```
cd /usr/share/openstack-dashboard/
python manage.py compress --force
python manage.py collectstatic --noinput
```
Restart Apache to activate the new panel:
```
sudo service apache2 restart
```

![alt text](https://raw.githubusercontent.com/cmer81/neutron-lbaas-dashboard-mirantis-mitaka/master/Capture%20du%202016-10-14%2021-47-24.png "screen 1")

![alt text](https://github.com/cmer81/neutron-lbaas-dashboard-mirantis-mitaka/blob/master/Capture%20du%202016-10-14%2021-47-57.png?raw=true "screen 2")
