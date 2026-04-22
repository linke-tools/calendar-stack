# Serve locally mirrored caldav data via RSS feed


## Clone and build the required docker images

    # IMAGES="calendarfeed httpcall pimsync sabredav"
    # for i in $IMAGES; do git clone https://github.com/linke-tools/$i-docker.git; done
    # for i in $IMAGES; do docker build --no-cache -t $i "${i}-docker"; done

## Configure and run the stack

* Clone this image with `git clone https://github.com/linke-tools/calendar-stack.git`
* `cd calendar-stack/`
* Copy `env.example` to `.env`
* Copy `.secrets.example` to `.secrets`
* Configure the variables in `.env` and `.secrets/*`

Create `/data` directory

    # mkdir -p data

Start the stack

    # docker compose up -d

Setup the frontend proxy

## Migration

The only statefull data to migrate are the connections between the keys and the internal calendar urls.

###  Export connected calendars from database

    # source .secrets/db-calendarfeed.env
    # docker exec calendar-stack-calendarfeed-1 sh -c "mysqldump -u $MYSQL_USER -p$MYSQL_PASSWORD -h db-calendarfeed calendarfeed" > calendarfeed.sql

### Import dump into fresh deployment

    # source .secrets/db-calendarfeed.env
    # docker exec -i calendar-stack-calendarfeed-1 sh -c "mysql -u $MYSQL_USER -p$MYSQL_PASSWORD -h db-calendarfeed calendarfeed" < calendarfeed.sql
