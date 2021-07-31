```zsh
~/desktop/redmine-reading
$ docker-compose up -d
redmine-reading_db_1 is up-to-date
Starting redmine-reading_web_1 ... done

~/desktop/redmine-reading
$ docker ps
CONTAINER ID   IMAGE                 COMMAND                  CREATED          STATUS          PORTS                    NAMES
097bab66e9ca   redmine-reading_web   "entrypoint.sh bash …"   27 minutes ago   Up 11 seconds   0.0.0.0:3003->3000/tcp   redmine-reading_web_1
43c16458e07a   postgres              "docker-entrypoint.s…"   27 minutes ago   Up 27 minutes   0.0.0.0:5433->5432/tcp   redmine-reading_db_1

~/desktop/redmine-reading
$ docker attach redmine-reading_web_1
Started GET "/" for 172.24.0.1 at 2021-07-31 02:58:28 +0000
Processing by WelcomeController#index as HTML
Creating scope :sorted. Overwriting existing method Group.sorted.
Creating scope :sorted. Overwriting existing method User.sorted.
  Setting Load (11.6ms)  SELECT "settings".* FROM "settings" WHERE "settings"."name" = $1 ORDER BY "settings"."id" DESC LIMIT $2  [["name", "session_lifetime"], ["LIMIT", 1]]
  Setting Load (1.2ms)  SELECT "settings".* FROM "settings" WHERE "settings"."name" = $1 ORDER BY "settings"."id" DESC LIMIT $2  [["name", "session_timeout"], ["LIMIT", 1]]
  Token Update All (19.2ms)  UPDATE "tokens" SET "updated_on" = $1 WHERE "tokens"."user_id" = $2 AND "tokens"."value" = $3 AND "tokens"."action" = $4  [["updated_on", "2021-07-31 02:58:31.365216"], ["user_id", 1], ["value", "c603649c94a6b62696ae64c68153cea3a3fb0d26"], ["action", "session"]]
   (1.3ms)  SELECT MAX("settings"."updated_on") FROM "settings"
  User Load (18.6ms)  SELECT "users".* FROM "users" WHERE "users"."type" IN ($1, $2) AND "users"."status" = $3 AND "users"."id" = $4 LIMIT $5  [["type", "User"], ["type", "AnonymousUser"], ["status", 1], ["id", 1], ["LIMIT", 1]]
  Current user: admin (id=1)
  Setting Load (2.8ms)  SELECT "settings".* FROM "settings" WHERE "settings"."name" = $1 ORDER BY "settings"."id" DESC LIMIT $2  [["name", "force_default_language_for_loggedin"], ["LIMIT", 1]]
  Setting Load (0.9ms)  SELECT "settings".* FROM "settings" WHERE "settings"."name" = $1 ORDER BY "settings"."id" DESC LIMIT $2  [["name", "force_default_language_for_anonymous"], ["LIMIT", 1]]

From: /redmine/app/controllers/welcome_controller.rb:25 WelcomeController#index:

    23:   def index
    24:         binding.pry
 => 25:     @news = News.latest User.current
    26:   end

[1] pry(#<WelcomeController>)>
```

http://localhost:3003/

Refs: [Redmineのコードリーディング用環境をDocker上に構築する](https://qiita.com/2bo/items/b9151bf7599b2b37d980)
