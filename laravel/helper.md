## Global helpers
> For global helper used in laravel `app/helpers.php` or `app/Http/helpers.php` add following in composer's autoload node.
```bash
"files": [
            "app/helpers.php"
        ]
```

## Packages
> Important or Recommanded packages for Laravel which most frequently using
1. For debugging `barryvdh/laravel-debugbar`
2. Pdf `barryvdh/laravel-dompdf`
3. Graphql `alexaandrov/laravel-graphql-client`
4. Page cache `silber/page-cache`
5. File-manager `unisharp/laravel-filemanager`
6. Image Manage & Upload `intervention/image`
7. Excel & Spreadsheet `maatwebsite/excel`
8. Role Permission `spatie/laravel-permission`

## Slack for Log
> You can add all of your project log to a specific slack channel through `channel webhook`

?> Go to your project `.env` file and add the following settings as
```text
LOG_CHANNEL=stack
LOG_SLACK_WEBHOOK_URL=`https://hooks.slack.com/services/TRR3YMWL2/BTFJ8G4RG/xxxxxxkxkxxkxkxxxxx
```
> Where `LOG_SLACK_WEBHOOK_URL` is the webhook key for the channel. 

> For slack workspace search for an Apps as `Incoming Webhooks`. When adding the apps just specify your desire channel. Finally you will get a webhook url.

!> For getting all the logs type like `info`,`debug`,`error` through webhook, go to `config/logging.php` and in `channels` section for `slack` set level `info` instead `debug`.