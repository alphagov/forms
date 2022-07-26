# GOV.UK Forms Development

This is a guide to getting the Gov.uk Forms development environment up and running.

list of github projects.

This repo lives at:
https://github.com/alphagov/forms

The express base prototype can be found at:
https://github.com/alphagov/forms-prototypes

and the static page which is behind https://www.forms.service.gov.uk/ can be found at:
https://github.com/alphagov/forms-product-page


The components which make up the service are:
https://github.com/alphagov/forms-runner
https://github.com/alphagov/forms-api
https://github.com/alphagov/forms-admin

## Commands for running the whole thing in docker.

You need to check out all three projects in the parent directory of this repo.
Your directory structure should look like this:

```
top-level/
├── forms-admin
├── forms-api
└── forms-runner
└── forms
    └── development
        ├── README.md
        └── docker-compose.yml
```

Then run:
```bash
docker-compose up
```

Wait a while as the images are downloaded and built. Eventually you should see the screen fill with logging information as the postgres, redis and the forms services start.

You should be able to open the admin interface on http://localhost:3000 , and the runner on http://localhost:3001

To stop the services from running, press `Ctrl-c` and then enter:
```bash
docker-compose stop
```

If you make changes to the docker file:

```bash
docker-compose up --build
```

## The override file
The override file shows an example or running services locally in addition to those defined in the docker-compose.yml file.
