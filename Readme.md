Docker to use Decidim
Docker image to deploy Decidim.

This docker image is based on ruby:2.6.5. It includes the packages needed to run Decidim (Especially NodeJS). The Decidim application is installed in folder /app and can be find in environment variable DECIDIM_PATH.

Getting Started
Prerequisities
Quickstart Demo
Quickstart
Environment Variables
Example : Run production version with external initialization script
Example : Run development version
Authors
License
Getting Started
Prerequisities
In order to run this container you'll need docker installed.

Windows
OS X
Linux
Quickstart Demo
To run a simple example, you can use the file docker-compose-demo.yml

version: '3'
services:
  app:
    image: pcourbin/decidim:0.28.2
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
and run

docker-compose -f docker-compose-demo.yml up
Then, go to http://localhost:3000 (after a long wait due to creation of seed data, you can check the logs docker-compose -f docker-compose-demo.yml logs -f) and login with the users defined for seed data by Decidim:

Path	User	Password	Description
http://localhost:3000/system	system@example.org	decidim123456	A Decidim::System::Admin to log in at /system.
http://localhost:3000	admin@example.org	decidim123456	A Decidim::User acting as an admin for the organization.
http://localhost:3000	user@example.org	decidim123456	A Decidim::User that also belongs to the organization but it’s a regular user.
Be careful, this a demo/test example. You can create a new organization, but you will not receive any email, even if you configure the SMTP server on the organization configuration page. So you will not be able to confirm any administrator or new user.
