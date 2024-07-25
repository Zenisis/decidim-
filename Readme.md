# Docker to use [Decidim](https://decidim.org/)

Docker image to deploy [Decidim](https://decidim.org/).

This docker image is based on [ruby:2.6.5](https://hub.docker.com/_/ruby).
It includes the packages needed to run [Decidim](https://github.com/decidim/decidim) (Especially [NodeJS](https://nodejs.org/)). The Decidim application is installed in folder `/app` and can be find in environment variable `DECIDIM_PATH`.

-   [Getting Started](#getting-started)
    -   [Prerequisities](#prerequisities)
    -   [Quickstart Demo](#quickstart-demo)
    -   [Quickstart](#quickstart)
-   [Environment Variables](#environment-variables)
-   [Example : Run production version with external initialization
    script](#example--run-production-version-with-external-initialization-script)
-   [Example : Run development
    version](#example--run-development-version)
-   [Authors](#authors)
-   [License](#license)

## Getting Started

### Prerequisities

In order to run this container you'll need docker installed.

* [Windows](https://docs.docker.com/windows/started)
* [OS X](https://docs.docker.com/mac/started/)
* [Linux](https://docs.docker.com/linux/started/)

### Quickstart Demo

To run a simple example, you can use the file `docker-compose-demo.yml`

```
version: '3'
services:
  app:
    image: pcourbin/decidim:0.20.0
    environment:
      - DATABASE_HOST=pg
      - DATABASE_USERNAME=decidim
      - DATABASE_PASSWORD=pgpassword
      - RAILS_ENV=development
      - DB_CREATE=true
      - DB_SEED_DATA=true
    ports:
      - 3000:3000
    links:
      - pg

  pg:
    image: postgres
    environment:
      - POSTGRES_USER=decidim
      - POSTGRES_PASSWORD=pgpassword
```
and run
```
docker-compose -f docker-compose-demo.yml up
```
Then, go to http://localhost:3000 (after a long wait due to creation of seed data, you can check the logs `docker-compose -f docker-compose-demo.yml logs -f`) and login with the users defined for [`seed data` by Decidim](https://docs.decidim.org/develop/en/getting_started/):

| Path | User | Password | Description |
| --- | --- | --- |--- |
| http://localhost:3000/system | system@example.org | decidim123456 | A Decidim::System::Admin to log in at /system. |
| http://localhost:3000 | admin@example.org | decidim123456 | A Decidim::User acting as an admin for the organization. |
| http://localhost:3000 | user@example.org | decidim123456 | A Decidim::User that also belongs to the organization but it’s a regular user. |

Be careful, this a demo/test example. You can create a new organization, but you will not receive any email, even if you configure the SMTP server on the organization configuration page. So you will not be able to confirm any administrator or new user.


 
    
   
 





     





## Authors
* **Pierre Courbin** - *Initial work* - [PCourbin](https://github.com/pcourbin)

## License
This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details.
