Add LBaaS panels to Dashboard Mitaka Mirantis!
===================


The Dashboard panels for managing ***LBaaS v2*** are available starting with the Mitaka **Mirantis** release.

----------


**On your Controller**
-------------

Clone the neutron-lbaas-dashboard repository and check out the release branch that matches the installed version of Dashboard:
```
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
