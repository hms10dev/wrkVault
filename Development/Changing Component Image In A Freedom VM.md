

For AWS VM - Refer [NO LONGER VALID: SSH Access To Freedom VMs (AWS)](https://manhattanassociates.atlassian.net/wiki/spaces/OM/pages/1105928494)

For GCP VM - Refer [SSH Access To Freedom VMs (GCP)](https://manhattanassociates.atlassian.net/wiki/spaces/OM/pages/1511851187)

- Switch to the super user
    

`sudo su`

- Navigate to the script path
    

`cd /manh/side/om-vm-auto-scripts/`

- Open the cattle.override.yml file
    

For components, you can even use cattle.yml file. But it is recommended to make the changes in cattle.override.yml.

The configuration for hazelcast, zuulserver and authserver are present in pets.yml file. If you want to change the image ID for one of these components, execute the steps using pets.yml in place of cattle.override.yml

`vi cattle.override.yml`

- Go to the line containing the component image
    
- Edit the file to replace _**${IMAGE_TAG}**_ with the required component image
    

Eg:

Assume the image ID required for order component is 50.000.0-fb41242-2105241451

The initial entry in cattle.override.yml file would look like → image: ${DOCKER_REGISTRY}com-manh-cp-order:${IMAGE_TAG}

The changed entry in cattle.override.yml file should look like → image: ${DOCKER_REGISTRY}com-manh-cp-order:50.000.0-fb41242-2105241451

- Save the file and exit the vi editor
    
- Get the container running the component image
    

`docker ps -a | grep <component_name>`

- Stop the docker container
    

`docker stop <container_id>`

- Remove the docker container
    

`docker rm <container_id>`

- Restart sidedeputy
    

`source env.sh && docker-compose -f pets.yml --compatibility restart sidedeputy`

- Bring up the application container
    

`source env.sh && docker-compose -f cattle.override.yml --compatibility up -d <component_name>`