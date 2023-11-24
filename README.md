# odoo-docker-instances
Odoo Docker Instances Configuration

Ready to use Odoo Docker Container (single/multiple instances)

----------------

## How To Use

- Clone this repository
- cd to odoo folder
- Make sure Docker & Docker Compose is installed
- Set the postgres environment in [docker-compose.yml](odoo/docker-compose.yml)
	+ POSTGRES_DB
	+ POSTGRES_USER
	+ POSTGRES_PASSWORD
- Set the odoo configuration in [odoo.conf](odoo/config/odoo.conf)
	+ admin_passwd : Odoo Master Password
	+ db_host : Postgres service name in [docker-compose.yml](odoo/docker-compose.yml) (ex: db)
	+ db_user : Postgres user (the same as postgres environment above)
	+ db_password : Postgres password (the same as above)
- Run `docker compose up -d`
- Open [http://127.0.0.1:8070/](http://127.0.0.1:8070)

- If it shows `Error 500` and the logs in `docker compose logs` shows "_Database not initialized_", Stop docker instance by running `docker compose stop`
- Run `docker compose run web bash` followed by `odoo --init base --database POSTGRESS_DB --stop-after-init --db_host=POSTGRESS_SERVICE_NAME --db_user POSTGRES_USER --db_password POSTGRES_PASSWORD`
- Exit bash and Run `docker compose restart`

## Multiple Instances

To run multiple instances, just duplicate the odoo folder and rename it to whatever you want. Follow the above instructions, and MAKE SURE to change the ports value (left side of the colon) in [docker-compose.yml](odoo/docker-compose.yml) both for odoo and postgres. Ex: odoo ports -> `"8071:8069"` and postgres ports -> `"5434:5432"`