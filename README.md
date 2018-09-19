homeassistant-apb
=========

Deploy [Home Assistant](https://www.home-assistant.io/) with either ephemeral
or persistent storage, along with a container for editing configuration files.

Intended to be consumed as an [Ansible Playbook
Bundle](http://automationbroker.io).

homeassistant-apb variables
--------------

    app_name: "homeassistant-apb-{{ _apb_service_instance_id.split('-')[0] }}"

Default application name when provisioning objects. Make sure this name does
not exceed 63 chars (less 18 characters if using GlusterFS due to persistent
volume dynamic name creation).

    app_image: docker.io/homeassistant/home-assistant:0.78.0

Container image and version to deploy.

    namespace: "{{ lookup('env','NAMESPACE') | default('home-assistant', true) }}"

Namespace the application will be deployed to.

Notes
-----

In order to make it easier to edit the `configuration.yaml` file without having
to figure out how to mount the persistent volume externally, a sidecar is
included running `vim` so that you can modify `configuration.yaml` and safely
execute a new deployment to restart the pod.

License
-------

Apache v2.0

Author Information
------------------

Leif Madsen (leif at leifmadsen dot com)
