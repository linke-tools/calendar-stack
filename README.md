# Serve locally mirrored caldav data via RSS feed


## Clone and build the required docker images



    # git clone https://github.com/linke-tools/httpcall-docker.git
    # git clone https://github.com/linke-tools/sabredav-docker.git
    # git clone https://github.com/linke-tools/pimsync-docker.git
    # git clone https://github.com/linke-tools/calendarfeed-docker.git

    # for i in calendarfeed httpcall pimsync sabredav; do docker build --no-cache -t $i "${i}-docker"; done

## Configure an run the stack

* Clone this image
* `cd calendar-stack/`
* Copy `env.example` to `.env`
* Copy `.secrets.example` to `.secrets`
* Configure the variables in `.env` and `.secrets/*`

Create `/data` direcoties

    # mkdir -p data/{certbot,db-calendarfeed}

Initialize the certficates whith

    # docker compose -f docker-compose-init.yml up

Start the stack

    # docker compose up -d
