## Creating the containers
Clone the xdmod repo to xdmod-src:

`git clone https://github.com/ubccr/xdmod-private.git xdmod-src/xdmod-private`

If you want your data shredded automatically on container start, follow the Load your data section - create the slurm_data folder first and populate with data.

Then build the images and start the containers:

`docker-compose up -d`

## Load your data

Put your data in slurm_data folder (and make it shareable) in format yyyymmdd. There's a helper script get_data.sh. Initially everything will be shredded and ingested automatically before running the web server. To view the progress you can run log watch:

`docker logs -f xdmoddocker_openxdmod_1`

To update the data for a new day, login to the container and trigger the shredding and ingesting processes:

`docker exec -it xdmoddocker_openxdmod_1 /bin/bash`

`/usr/share/xdmod/bin/xdmod-shredder -r Comet -f slurm -d /var/slurm_data`

`/usr/share/xdmod/bin/xdmod-ingestor`
