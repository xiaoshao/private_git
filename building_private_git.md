# How to build a private git server with gitlab
---

1. start a postgresql server
	```
	 docker run --name gitlab-postgresql -d \
    	--env 'DB_NAME=gitlabhq_production' \
    	--env 'DB_USER=gitlab' --env 'DB_PASS=password' \
    	--env 'DB_EXTENSION=pg_trgm' \
    	--volume /srv/docker/gitlab/postgresql:/var/lib/postgresql \
    	sameersbn/postgresql:9.5-3
	```

2. start a redis server
	```
	docker run --name gitlab-redis -d \
    	--volume /srv/docker/gitlab/redis:/var/lib/redis \
    	sameersbn/redis:latest
	```

3. startup gitlab server
	```
	docker run --name gitlab -d \
    	--link gitlab-postgresql:postgresql --link gitlab-redis:redisio \
    	--publish 10022:22 --publish 10080:80 \
    	--env 'GITLAB_PORT=10080' --env 'GITLAB_SSH_PORT=10022' \
    	--env 'GITLAB_SECRETS_DB_KEY_BASE=long-and-random-alpha-numeric-string' \
    	--env 'GITLAB_SECRETS_SECRET_KEY_BASE=long-and-random-alpha-numeric-string' \
    	--env 'GITLAB_SECRETS_OTP_KEY_BASE=long-and-random-alpha-numeric-string' \
    	--env 'GITLAB_HOST=10.38.34.223' \
    	--volume /srv/docker/gitlab/gitlab:/home/git/data \
    	sameersbn/gitlab:8.13.6
	```

The files `/srv/docker/gitlab/` will be kept on the laptop. You have to backup it as frequent as possible to protect it from disasters.
