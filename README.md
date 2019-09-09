# Ansible Role: Jenkins

[![Build Status](https://travis-ci.org/aem-design/ansible-role-jenkins.svg?branch=master)](https://travis-ci.org/aem-design/ansible-role-jenkins)

Setup jenkins in your environment.
> This role was developed as part of
> [AEM.Design](http://aem.design/)

## Requirements

None.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

| Name                       	| Required 	| Default                                                                   	| Notes                       	|
|----------------------------	|----------	|---------------------------------------------------------------------------	|-----------------------------	|
| docker_image_user          	|          	| aemdesign                                                                 	|                             	|
| docker_image_name          	|          	| jenkins                                                                   	|                             	|
| docker_image               	|          	| {{ docker_image_user }}/{{ docker_image_name }}                           	|                             	|
| docker_image_tag           	|          	| latest                                                                    	|                             	|
| docker_container_name      	|          	| jenkins                                                                   	|                             	|
| service_jenkins_http_port  	|          	| 8080                                                                      	|                             	|
| service_jenkins_agent_port 	|          	| 50000                                                                     	|                             	|
|                            	|          	|                                                                           	|                             	|
| service_jvm_opts           	|          	| -Dhudson.security.HudsonPrivateSecurityRealm.ID_REGEX=[a-zA-Z0-9_.@-]+    	| allow more chars in user id 	|
|                            	|          	|                                                                           	|                             	|
| docker_published_ports     	|          	|                                                                           	|                             	|
|                            	|          	| - "0.0.0.0:{{ service_jenkins_http_port | default('8080') }}:8080/tcp"    	|                             	|
|                            	|          	| - "0.0.0.0:{{ service_jenkins_agent_port | default('50000') }}:50000/tcp" 	|                             	|
|                            	|          	|                                                                           	|                             	|
| docker_volumes             	|          	|                                                                           	|                             	|
|                            	|          	| - "jenkins-data:/var/jenkins_home:z"                                      	|                             	|
|                            	|          	|                                                                           	|                             	|
| docker_container_user      	|          	| {{ docker_container_name }}                                               	|                             	|
| docker_container_userid    	|          	| 10001                                                                     	|                             	|
| docker_container_group     	|          	| {{ docker_container_name }}                                               	|                             	|
| docker_container_groupid   	|          	| 10001                                                                     	|                             	|
|                            	|          	|                                                                           	|                             	|
| iptable_rules              	|          	|                                                                           	|                             	|
|                            	|          	| - port: "{{ service_jenkins_http_port | default('8080') }}"               	|                             	|
|                            	|          	| comment: "service_jenkins_http_port"                                      	|                             	|
|                            	|          	| - port: "{{ service_jenkins_agent_port | default('50000') }}"             	|                             	|
|                            	|          	| comment: "service_jenkins_agent_port"                                     	|                             	|


## Dependencies

This role depends on roles:
 
- `aem_design.docker_container`

## Example Playbook

```yaml
- hosts: all
  roles:
    - { role: aem_design.jenkins
    }
```

## License

Apache 2.0

## Author Information

This role was created by [Max Barrass](https://aem.design/).