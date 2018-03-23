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
|`user_gogs_admin`      | `gogs`        | Admin username to create in Gogs |
|`user_gogs_test`       | `test`        | Test username to create in Gogs |
|`user_gogs_password`   | `openshift`   | Gogs password to configure for admin and test users |
|`labs_github_ref`      | `master`      | GitHub branch to user for lab code https://github.com/openshift-labs/devops-oab-labs.git |
|`user_count`           | 10            | Number of users for generating DEV, STAGE and PROD projects |
|`user_format`          | `user%02d`    | [printf style format](https://en.wikipedia.org/wiki/Printf_format_string) for OpenShift users that __already exist__ in the cluster |
|`openshift_prod_master`| -             | Master url for PROD, if using a separate cluster for PROD |
|`openshift_prod_token` | -             | Auth token for PROD, if using a separate cluster for PROD |


How To Use
------------

```
ansible-galaxy install -r requirements.yml
ansible-playbook init.yml -e "user_count=50"
```

If using a separate DEV and PROD OpenShift clusters in the labs:
```
ansible-galaxy install -r requirements.yml
ansible-playbook init.yml -e "user_count=50" \
                          -e "openshift_prod_master=http://prod.myopenshift.com" \
                          -e "openshift_prod_token=..."
```