Ansible Playbook For Workshop Setup
=========

The provided playbook automates preparing an OpenShift cluster for the DevOps and Ansible 
workshop by creating the required projects, configurations and supporting pods (Git, etc) which 
are used during the labs.

The playbook also generates a test user in Gogs and initializes the projects for this user in 
order to simplify test-running the labs.


Playbook Variables
------------

| Variable              | Default Value | Description   |
|-----------------------|---------------|---------------|
|`lab_infra_project`    | `lab-infra`   | Project name to deploy Git server and lab guides  |
|`project_admin`        | `student`     | OpenShift user to set as admin for projects |
|`user_gogs_admin`      | `gogs`        | Admin username to create in Gogs |
|`user_gogs_test`       | `test`        | Test username to create in Gogs |
|`user_gogs_password`   | `openshift`   | Gogs password to configure for admin and test users |
|`labs_github_ref`      | `master`      | GitHub branch to user for lab code https://github.com/openshift-labs/devops-oab-labs.git |
|`configure_broker`     | `true`        | Configure Ansible Broker for Digital Ocean APBs. Needs cluster admin |
|`clean_init`           | `false`       | Clean the environment and remove projects before init |

How To Run
------------

```
ansible-galaxy install -r requirements.yml
ansible-playbook init.yml
```

Troubleshooting
------------

* Ansible on Mac OS X needs the GNU tar instead of BSD tar. Install it via `brew install gnu-tar`


Tips
----------------
* Pre-pull images on all nodes

  ```
  docker pull registry.access.redhat.com/redhat-openjdk-18/openjdk18-openshift:1.2
  docker pull registry.access.redhat.com/rhscl/nodejs-4-rhel7:latest
  docker pull registry.access.redhat.com/openshift3/jenkins-2-rhel7:latest
  docker pull registry.access.redhat.com/openshift3/jenkins-slave-maven-rhel7:latest
  docker pull registry.access.redhat.com/rhscl/mysql-57-rhel7
  docker pull registry.access.redhat.com/openshift3/ose-deployer
  docker pull registry.access.redhat.com/openshift3/ose-sti-builder
  docker pull sonatype/nexus3:3.7.1
  docker pull openshiftdemos/gogs:0.11.34
  docker pull osevg/workshopper:latest
  docker pull siamaksade/rhsummit18-devops-web

  ```

* Add an admin user to the cluster. Run the following as `system:admin`:

  ```
  oc adm policy add-cluster-role-to-user cluster-admin admin
  ```
